# Aircraft 多机规则冲突仿真器

本项目是面向多飞行器协同决策的决策级仿真器与安全仲裁实验代码。系统在局部观测和通信不完整条件下运行名义多智能体策略，并通过在线信念 STL 监测、规则—智能体依赖关系和连续残差安全优化处理规则冲突。

当前仓库对应论文 `Aircraft--v6.0.docx` 的最终代码版本。旧论文归档为 `Aircraft--v6.0_old.docx`，不参与实验入口。

## 主要模块

```text
aircraft_sim/
  env.py          决策级多机环境与局部观测
  rules.py        真值规则监测和规则语义
  belief.py       在线信念更新、违约概率和 STL 鲁棒度
  rule_graph.py   规则—智能体依赖图与冲突记录
  qp_shield.py    动态仲裁和连续残差 QP/SQP 安全层
  mappo.py        本文策略的 MAPPO 风格训练与更新接口
  evaluation.py   统一评测指标和轨迹记录
  scenarios.py    冲突场景模板
  baselines.py    训练型基线策略
external_adapters/   官方方法适配器
external_methods/    第三方方法源码入口
tests/               回归测试
results/             实验结果和可追溯日志
```

本文方法的在线流程为：

```text
局部观测
  -> 信念更新与规则概率估计
  -> 规则—智能体依赖图
  -> 动态优先级离散仲裁
  -> 连续残差 QP/SQP
  -> 执行安全动作与冲突日志
```

动作集合为 `HOLD`、`SUPPORT`、`COVER`、`RECOVER`、`EXIT` 和 `CRITICAL`。环境真值只用于离线评测，安全层的在线输入为局部观测和通信历史。

## 环境安装与测试

建议使用 Python 3.10 或更高版本，并安装项目依赖：

```powershell
python -m pip install numpy scipy torch pytest
python -m pytest -q
```

当前回归测试覆盖环境、规则、在线信念、QP 安全层、训练接口和实验协议。最终版本通过 70 个测试。

## 最终实验协议

完整协议入口为：

```powershell
.\run_final_protocol.ps1
```

该脚本依次运行回归测试、本文方法十种子训练、七种方法十种子对比、冲突消融和 JSBSim 验证。完整结果统一保存到：

```text
results/final_protocol_20261007/
```

主要结果目录如下：

```text
official_10seed/                       七种方法十种子主实验
proposed_10seed/                       本文方法训练、checkpoint 和训练记录
conflict_10seed/                       原四类冲突消融
component_ablation_10seed/             依赖图、动态优先级和连续 QP 受控消融
calibration_10seed_fixed/              风险校准实验
short_recovery_paper_protocol_10seed/  第 6.5 节高冲突短期压力测试
jsbsim_10seed/                         JSBSim F-16 六自由度验证
conflict_traces_seed11/                真实冲突案例逐步日志
```

主实验重点文件包括 `summary.json`、`per_seed.json`、`per_episode.json` 和 `manifest.json`。统计汇总目录同时保存 `paper_table.md`、配对差值和完整 JSON 数据，便于复核论文表格。

## 基线与官方代码

MAPPO 官方仓库固定为 `marlbenchmark/on-policy` 的 commit：

```text
de66d7a4b23fac2513f56f96f73b3f5cb96695ac
```

MACPO 官方仓库固定为 `chauncygu/Multi-Agent-Constrained-Policy-Optimisation` 的 commit：

```text
b80a9f5b4a0049125a827be8fb9c477f69ae021b
```

主对比方法包括本文方法、MAPPO、HAPPO、HATRPO、MACPO、MAPPO-Lagrangian 和 MAT。MAT 使用集中式联合信息，只作为理想信息条件下的参考上界；其信息假设不等同于本文和其他分散执行方法。

训练型基线入口：

```powershell
python run_trainable_baselines.py `
  --methods proposed_belief_stl_conflict_qp `
  --seeds 11 22 33 44 55 66 77 88 99 111 `
  --updates 100 --episodes 40 --horizon 30 `
  --warmstart-epochs 100 `
  --output results/proposed_10seed
```

官方方法对比入口：

```powershell
python run_official_comparison.py `
  --seeds 11 22 33 44 55 66 77 88 99 111 `
  --updates 100 --episodes 40 --horizon 30 `
  --ppo-epoch 5 --checkpoint-interval 5 `
  --line-search-steps 10 --safety-bound 0.1 `
  --proposed-results results/proposed_10seed `
  --output results/official_10seed
```

## 组件消融

`run_component_ablation.py` 对四种配置使用相同场景、策略和随机种子：

| 配置 | 依赖图 | 动态优先级 | 连续残差 QP |
|---|---:|---:|---:|
| DG-QP | 是 | 是 | 是 |
| No-Graph | 否 | 是 | 是 |
| Fixed-Priority | 是 | 否 | 是 |
| Gate-Only | 是 | 是 | 否 |

组件消融只分析每个组件的受控净收益，不替换主实验结果：

```powershell
python run_component_ablation.py `
  --seeds 101 202 303 404 505 606 707 808 909 1001 `
  --horizon 30 --initial-feasible-only `
  --output results/component_ablation_10seed

python analyze_component_ablation.py `
  --input results/component_ablation_10seed/per_seed.json `
  --output results/component_ablation_10seed/statistical_summary
```

## 动态优先级受控激活实验

该实验是独立的机制验证，不修改主实验、原八类场景或安全层默认行为。它构造同一智能体同时面对 `I02` 信息规则和 `F04` 资源规则的状态，比较动态优先级与固定 P0--P5 顺序的离散仲裁动作。

```powershell
python run_dynamic_priority_activation.py `
  --seeds 101 202 303 404 505 606 707 808 909 1001 `
  --horizon 10 `
  --output results/final_protocol_20261007/dynamic_priority_activation_10seed

python analyze_dynamic_priority_activation.py `
  --input results/final_protocol_20261007/dynamic_priority_activation_10seed/per_seed.json `
  --output results/final_protocol_20261007/dynamic_priority_activation_10seed/statistical_summary
```

该实验的主要终点是规则同时激活时的离散动作差异率，而不是总体 Reward 或安全率提升。这样可以把动态优先级的机制作用与主实验的总体性能结论区分开。

## 高保真验证

JSBSim 验证入口为：

```powershell
python run_high_fidelity_validation.py --backend jsbsim
```

如本机未安装 JSBSim 或缺少 F-16 飞行器 XML，程序会明确报告依赖问题。`surrogate` 后端只能用于跨动力学趋势检查，不能替代 JSBSim 六自由度结果。

## 复现原则

所有正式实验应保留命令参数、随机种子、方法配置、逐种子结果和运行日志。结果目录中的 `manifest.json` 记录协议版本和关键参数；论文中的统计表应从对应结果目录重新生成，而不是手工修改旧表。

安全层在线计算使用 `numpy`、`scipy` 和 `torch`。当前环境是决策级多机仿真器，不能将其表述为已经完成真实飞控认证或实机部署验证。
