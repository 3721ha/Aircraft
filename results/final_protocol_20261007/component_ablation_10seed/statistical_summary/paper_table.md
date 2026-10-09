# Controlled component ablation

All variants use the same full rule reports, templates, seeds and nominal policy.
Positive `delta_better` means the complete DG-QP is better than the ablation for that metric.

## Seed-level summary

| Variant | Reward | Joint STL | Truth hard violation | Target success | Intervention/step | Online ms | QP fallback |
|---|---:|---:|---:|---:|---:|---:|---:|
| DG-QP | 26.2848 +/- 0.2271 | 0.5625 +/- 0.0471 | 0.0483 +/- 0.0123 | 0.7625 +/- 0.0283 | 1.5167 +/- 0.0364 | 12.2596 +/- 2.8211 | 0.0483 +/- 0.0116 |
| No-Graph | 26.2848 +/- 0.2271 | 0.5625 +/- 0.0471 | 0.0483 +/- 0.0123 | 0.7625 +/- 0.0283 | 1.5167 +/- 0.0364 | 12.3979 +/- 2.5799 | 0.0483 +/- 0.0116 |
| Fixed-Priority | 26.2848 +/- 0.2271 | 0.5625 +/- 0.0471 | 0.0483 +/- 0.0123 | 0.7625 +/- 0.0283 | 1.5167 +/- 0.0364 | 11.9028 +/- 2.4191 | 0.0483 +/- 0.0116 |
| Gate-Only | 26.2865 +/- 0.2228 | 0.5500 +/- 0.0462 | 0.0504 +/- 0.0138 | 0.7625 +/- 0.0283 | 1.4833 +/- 0.0393 | 0.6341 +/- 0.0739 | N/A |

## Paired component net benefits

| Component removed | Metric | N seeds | Delta (better direction) | 95% CI half-width | Sign-test p |
|---|---|---:|---:|---:|---:|
| dependency_graph | mean_reward | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | joint_satisfaction_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | conditional_joint_satisfaction_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | post_truth_hard_violation_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | target_hard_success_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | mean_intervention_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | mean_online_time_ms | 10 | -0.1383 | 0.5352 | 0.7539 |
| dependency_graph | qp_infeasible_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dependency_graph | rule_rule_conflict_step_rate | 10 | 0.5175 | 0.0382 | 0.0020 |
| dependency_graph | rule_rule_resolution_rate | 10 | 0.8295 | 0.0630 | 0.0020 |
| dynamic_priority | mean_reward | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | joint_satisfaction_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | conditional_joint_satisfaction_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | post_truth_hard_violation_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | target_hard_success_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | mean_intervention_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | mean_online_time_ms | 10 | 0.3568 | 0.7140 | 1.0000 |
| dynamic_priority | qp_infeasible_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | rule_rule_conflict_step_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| dynamic_priority | rule_rule_resolution_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| continuous_qp | mean_reward | 10 | -0.0018 | 0.0145 | 0.7539 |
| continuous_qp | joint_satisfaction_rate | 10 | 0.0125 | 0.0283 | 1.0000 |
| continuous_qp | conditional_joint_satisfaction_rate | 10 | 0.0125 | 0.0283 | 1.0000 |
| continuous_qp | post_truth_hard_violation_rate | 10 | 0.0021 | 0.0029 | 0.2500 |
| continuous_qp | target_hard_success_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| continuous_qp | mean_intervention_rate | 10 | 0.0333 | 0.0056 | 0.0020 |
| continuous_qp | mean_online_time_ms | 10 | 11.6255 | 2.7847 | 0.0020 |
| continuous_qp | qp_infeasible_rate | 0 | 0.0000 | 0.0000 | 1.0000 |
| continuous_qp | rule_rule_conflict_step_rate | 10 | 0.0000 | 0.0000 | 1.0000 |
| continuous_qp | rule_rule_resolution_rate | 10 | -0.0082 | 0.0078 | 0.0703 |
