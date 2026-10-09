# Aircraft 仿真器原型

这是一个与 `note2.md` / `paper_note.md` 对齐的决策级多机仿真器原型。它把专家知识落成可执行接口，并保留部分可观测条件下的双监测器边界：

- `AircraftEnv`：三维质点动力学、资源/能量、通信丢失、传感器噪声和局部观测。
- `RuleMonitor.evaluate_truth`：只读完整真值，用于离线评测。
- `RuleMonitor.evaluate_observation`：兼容旧版的确定性局部规则检查。
- `BeliefSTLMonitor`：基于局部观测/通信历史的高斯信念更新，输出违反概率和保守鲁棒度下界。
- `ConflictAwareQPSafetyShield`：硬规则优先、软规则可松弛的联合残差 QP/SQP 安全层；显式记录冲突和不可行回退。
- `SafetyShield`：对名义高层动作做最小残差修正；没有硬安全可行动作时进入 `RECOVER` 回退。
- `scenarios.py`：边界、通信中断、低资源、低识别置信度和多机冲突场景模板。

运行：

```powershell
python run_sim.py
python run_rollout.py
```

动作语义是 `HOLD`、`SUPPORT`、`COVER`、`RECOVER`、`EXIT`、`CRITICAL`，后续可将名义动作来源替换为 MAPPO，而不改变环境、规则和安全层接口。

`RolloutCollector` 同时保存名义动作和屏蔽后的执行动作，供干预一致学习使用；`ObservationEncoder` 输出固定维度向量，`ActionCodec` 完成策略向量和语义动作之间的转换。

训练示例：

```powershell
python run_train.py
python run_experiment.py
```

`MAPPOPolicy` 使用共享 actor 和集中式 critic，PPO 更新中包含安全层动作蒸馏损失，减少后续运行时干预。

可训练安全基线的统一烟雾实验：

```powershell
python run_trainable_baselines.py --seeds 11 --updates 2 --episodes 4 --horizon 10 --warmstart-epochs 10 --output results/trainable_baselines_smoke
```

正式运行时增加种子、更新数和测试回合数。该入口包含无约束 MAPPO、固定惩罚、STL 奖励、
Lagrangian、内部 MACPO 参考、短时域物理 CBF-QP/SQP 和完整方法。内部参考用于接口验证，不能替代
待接入的第三方官方实现。

官方 MAPPO 已固定为 `marlbenchmark/on-policy` commit
`de66d7a4b23fac2513f56f96f73b3f5cb96695ac`，第三方目录保持只读式原样，Aircraft 适配代码位于
`external_adapters/official_mappo.py`。最小闭环命令：

```powershell
python run_official_mappo.py --seeds 11 --updates 1 --episodes 4 --horizon 4 --control-bins 5 --ppo-epoch 1 --output results/official_mappo_smoke
```

这条命令只验证官方 actor、critic、buffer、PPO 更新和 checkpoint 重载，不构成正式性能结果。

官方约束 MARL 已固定到
`chauncygu/Multi-Agent-Constrained-Policy-Optimisation` commit
`b80a9f5b4a0049125a827be8fb9c477f69ae021b`。MACPO 和 MAPPO-Lagrangian 的最小闭环命令为：

```powershell
python run_official_macpo.py --seeds 11 --updates 1 --episodes 2 --horizon 3 --ppo-epoch 1 --line-search-steps 2 --output results/official_macpo_smoke
python run_official_mappo_lagrangian.py --seeds 11 --updates 1 --episodes 2 --horizon 3 --ppo-epoch 1 --output results/official_mappo_lagrangian_smoke
python run_official_happo.py --seeds 11 --updates 1 --episodes 2 --horizon 3 --ppo-epoch 1 --output results/official_happo_smoke
python run_official_hatrpo.py --seeds 11 --updates 1 --episodes 2 --horizon 3 --line-search-steps 2 --output results/official_hatrpo_smoke
python run_official_mat.py --seeds 11 --updates 1 --episodes 2 --horizon 3 --ppo-epoch 1 --output results/official_mat_smoke
```

正式外部对比默认统一使用连续 `Box(5)` 潜动作和轨迹级硬规则二值代价。早期采用离散 MAPPO
动作或逐步 MACPO 成本的结果属于诊断实验，不能直接放入最终公平对比表。

六种完整规则官方方法可由同一入口按共享训练/验证/测试协议运行。`--resume` 只复用参数完全匹配且
结果文件完整的方法，长实验中断后可以续跑：

```powershell
python run_trainable_baselines.py --methods proposed_belief_stl_conflict_qp --seeds 11 22 33 44 55 --updates 100 --episodes 40 --horizon 30 --warmstart-epochs 100 --output results/proposed_official_protocol
python run_official_comparison.py --seeds 11 22 33 44 55 --updates 100 --episodes 40 --horizon 30 --resume --proposed-results results/proposed_official_protocol --output results/official_comparison
```

第二条命令会校验本文方法的种子、预算和检查点选择口径，并生成“本文方法 + 六种官方对照”的七行主表源数据；
旧版 `trainable_baselines` 结果不满足新外部协议时会被明确拒绝，不能静默混入。

GCBF+ 是仅处理 S01/S02/S03 的物理安全屏蔽器，必须在独立 Python 3.10/JAX 环境运行并单列专项表，
不能把它的物理规则满足率与上述方法的完整规则联合满足率混入一张表。安装和运行步骤见
`external_methods/inbox/gcbfplus/REPO_INFO.md`。

正式结果完成后可直接生成论文表格和配对审计，不会重新训练：

```powershell
python analyze_official_results.py --results results/official_comparison
```

输出 `main_table.csv/.md`、`paired_comparison.json` 和 `scenario_breakdown.csv/.json`。

冲突核心创新的聚焦实验只保留初始真值可行、运行中触发规则冲突的模板，并报告目标硬规则成功率：

```powershell
python run_conflict_arbitration_experiments.py --seeds 101 202 303 404 505 606 707 808 909 1001 --horizon 30 --initial-feasible-only --output results/conflict_arbitration_focus
python analyze_conflict_arbitration.py --input results/conflict_arbitration_focus/per_seed.json --output results/conflict_arbitration_focus/statistical_summary
```

其中 `hard_target_rule_violation_count_per_step` 只统计 P0--P2 硬规则，`soft_target_rule_violation_count_per_step`
单独统计协同/任务连续性残差；`target_hard_success_rate` 是整条轨迹无硬目标违规的比例，`initial_feasible_rate`
用于确认样本不是从一开始就不可行。分析脚本同时生成 `paper_table.md/.csv` 和 `excluded_cases.json`；双支援这类
结构性不可同时满足的模板，应结合仲裁事件和保留的软规则残差解释，不能单独以目标成功率判定算法失败。

主表中的 `Actor inference ms` 是所有方法生成名义动作的平均墙钟时间；`Shield online ms` 是安全层
`filter` 的平均墙钟时间。无安全层基线的 Shield 列显示为 0，仅表示未调用安全层，不代表策略推理为 0。

QP/SQP 残差求解依赖 `numpy`、`scipy` 和 `torch`；当前实现仍是决策级仿真，不代表六自由度飞控认证。

可用 `python run_high_fidelity_validation.py --backend surrogate --include-mappo --updates 20` 运行固定策略和 MAPPO 的迁移验证。该验证代理增加执行器滞后和控制变化率限制，输出会明确标注 `lagged_3dof_validation_proxy`；它用于论文中的跨动力学趋势检查，不能替代 JSBSim/六自由度验证。若要尝试 JSBSim，请先单独安装可选 `jsbsim` 依赖并准备飞行器 XML，随后使用 `--backend jsbsim`，缺少配置时程序会显式停止。

论文实验口径、基线、场景划分和指标定义见 [`EXPERIMENT_PROTOCOL.md`](EXPERIMENT_PROTOCOL.md)。

`run_experiment.py` 在冻结场景集上比较无屏蔽名义策略、屏蔽策略、保守策略和 MAPPO 策略，并生成 `results/benchmark.json`、`results/benchmark.csv`、`results/pareto_front.json` 与 `results/training_curve.json`。评估结果区分干预前触发、干预后残余风险、规则冲突、重规划触发、QP 不可行回退率和平均在线求解时间。
