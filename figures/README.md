# Aircraft 论文图表资产索引

本目录按照论文大纲组织。所有 PNG 均为深色背景高分辨率版本，SVG 用于后续排版编辑。机制图只说明算法结构；带有 `case`、`seed`、`t` 的案例图来自真实逐步日志；统计图来自对应 `results` 目录。

## 01_framework：研究问题与仿真器

| 文件 | 建议标题 | 性质 |
|---|---|---|
| `fig01_research_mindmap` | 局部观测多飞行器规则冲突仲裁研究结构图 | 方法总览 |
| `fig02_online_closed_loop` | 本文方法的在线闭环 | 机制图 |
| `fig03_two_layer_simulator` | 决策级训练与 JSBSim 六自由度验证架构 | 已实现架构 |
| `fig04_rule_priority_pyramid` | 六级规则知识库与仲裁优先级 | 规则定义 |
| `fig05_online_computation_chain` | 名义策略、belief-STL、规则图与 QP 计算链 | 机制图 |

## 02_core_mechanism：核心创新

| 文件 | 建议标题 | 数据来源 |
|---|---|---|
| `fig06_belief_calibration` | 留出种子上的 belief 风险校准 | `paper_artifacts_10seed/risk_calibration_holdout.json` |
| `fig07_dependency_graph_mechanism` | 规则—智能体依赖图的构建与仲裁 | 机制图，明确标注 |
| `fig08_dependency_graph_actual` | C03:0 与 S03:0-1 的真实依赖图 | `support_separation, seed=11, t=0` |
| `fig09_dynamic_priorities` | 五类真实冲突的动态优先级 | 逐步规则图事件 |
| `fig10_qp_geometry` | QP 最小残差动作修正 | 几何示意，图内标注 |
| `fig11_intervention_consistent_training` | 干预一致训练与测试时外挂 QP | 机制图 |
| `fig12_conflict_method_outcome_matrix_shared_qp` | 五类冲突 × 七种冻结策略接入同一共享 QP | `step_trace.json` 的代表时间步 |
| `fig13_conflict_method_outcome_matrix_policy_only` | 五类冲突 × 七种原生策略（无共享 QP） | `step_trace.json` 的代表时间步 |

## 03_real_cases：真实冲突案例

| 文件 | 案例 |
|---|---|
| `fig14_case_a_scene` | F01 失联恢复与 C05 意图共享 |
| `fig15_case_a_solution` | 案例 A 四阶段求解过程 |
| `fig16_case_a_timeline` | 案例 A 的 t=0–7 时间线 |
| `fig17_case_a_methods` | 案例 A 的方法动作对比 |
| `fig18_case_b_scene` | I02/I03 信息条件与 M02 期限 |
| `fig19_case_b_arbitration` | 案例 B 的优先级仲裁 |
| `fig20_case_c_dual_support` | 两个 C03 请求竞争唯一支援者 |
| `fig21_case_d_trajectory` | C03 支援与 S03 安全趋势的轨迹修正 |
| `fig22_case_d_timeline` | 案例 D 七步最小间隔 |
| `fig23_case_e_resource_coverage` | F04 低资源与 C02 覆盖仲裁 |
| `fig25_case_e_belief_delay` | F04 belief 触发延迟 |

## 04_experiments：统计实验

| 文件 | 数据来源 |
|---|---|
| `fig26_conflict_ablation` | `conflict_arbitration_10seed/summary.json` |
| `fig27_short_horizon_recovery` | `recoverable_conflict_density_10seed/summary.json` |
| `fig28_main_results` | `official_comparison_10seed/summary.json` |
| `fig29_reward_safety_pareto` | 同上 |
| `fig30_jsbsim_zero_shot` | `high_fidelity_shield_attribution_10seed/summary.json` |
| `fig31_jsbsim_qp_attribution` | 同上 |
| `fig32_scalability` | `scale_experiments_stress_partitioned_final/summary.json` |

## 05_tables：可编辑表格

- `table01_method_capability`：方法能力比较。
- `table04_state_action`：状态、观测与动作定义。
- `table06_rule_hierarchy`：六级规则知识库。
- `table10_core_conflict_cases`：五类真实冲突的仲裁、残差和后果，提供 PNG/SVG/CSV/Markdown。
- `table11_all_methods_conflict_steps`：五个真实场景、七种方法、代表时间步的实际动作和真值记录，提供 CSV/Markdown。
- `table11a`～`table11e`：五个场景各自的七方法动作、核心规则后果和 QP 状态，提供 PNG/SVG/CSV/Markdown；这些表采用“冻结策略 + 同一共享 QP”归因口径。
- `table11_policy_only_conflict_steps`：不接共享 QP 的策略原生动作与结果，用来区分策略学习效果和安全层贡献。
- `table09_belief_calibration`：留出种子风险校准结果。
- `table20_conflict_ablation`：冲突仲裁安全层消融结果。
- `table21_short_recovery`：不同初始距离下的 3 步恢复结果。
- `table23_jsbsim_zero_shot`：JSBSim zero-shot 代表性结果。
- `table22_main_10seed`：正式十种子主结果，提供 PNG/SVG/CSV/Markdown。
- `table24_claims_limits`：可以支持与不能过度宣称的结论边界。

## 使用边界

1. 单步案例用于解释机制，不替代多随机种子统计。
2. `fig10_qp_geometry` 是几何示意，不是某一步求解平面的实测重建。
3. MAT 使用集中式联合信息，图表中保留为理想信息参考，不应写成完全同部署条件的基线。
4. JSBSim 结果是公开 F-16 六自由度仿真，不是硬件在环或真实飞行试验。
5. 支援—安全案例在 `t=3` 确实发生一次 S02 硬违规，图表未隐藏该失败点。

## 重生成

```powershell
.venv-gcbf\Scripts\python.exe generate_paper_assets.py
.venv-gcbf\Scripts\python.exe generate_paper_assets_supplement.py
```
