# Next-step experiment report

This report records completed smoke/protocol validation runs. These runs verify
the execution path and comparison controls; the one-seed, one-update results
are not final multi-seed performance evidence.

## Completed commands

### Test suite

- Command: `pytest -q`
- Exit status: `0` after adding `pythonpath = .` to `pytest.ini`.
- Result: `125 passed in 27.86s`.
- Command: `python -m pytest -q`
- Exit status: `0`
- Result: `125 passed in 27.94s`.

### RCC mechanism evaluation

- Command: `python run_rcc_mechanism_evaluation.py --seed 41 --aircraft 2 --horizon 4 --output results/next_step_mechanism`
- Exit status: `0`.
- Result paths: `results/next_step_mechanism/summary.json` and
  `results/next_step_mechanism/per_episode.json`.
- Fixed variables: seed `41`, 2 aircraft, horizon `4`, untrained controller
  (evaluation-path validation only).
- Coverage: actor-only and actor+projection on `train` (3 scenarios) and
  `unseen` (2 scenarios); counterfactual rule compositions
  `coverage_resource`, `coverage_separation`, `coverage_support`, and
  `coverage_support_priority_swapped`.
- Key metrics: train task return `-23.1263` (actor-only) vs `-23.1262`
  (actor+projection); unseen task return `-23.8814` vs `-23.6320`;
  hard-violation rate `0.0` on train and `0.125` on unseen for both methods;
  counterfactual unique nominal joint actions `4`, composition sensitivity
  `1.0`, priority sensitivity `1.0`.

## Completed commands

### RCC fixed-budget ablations

- Command: `python run_rcc_ablations.py --variants rcc_full rcc_no_task_commitment rcc_no_counterfactual rcc_no_projection --seeds 11 --updates 1 --horizon 4 --aircraft 2 --task interception --hidden 32 --epochs 1 --output results/next_step_ablations`
- Exit status: `0`.
- Result paths: `results/next_step_ablations/summary.json`,
  `per_seed.json`, `per_episode.json`, `training_trace.json`, and
  `control_audit.json`.
- Fixed variables: interception task, seed `11`, 2 aircraft, horizon `4`,
  one update, one PPO epoch, hidden width `32`; expected training budget is
  `4` environment steps per variant.
- Control audit: `passed=true`; all four variants observed `4` steps and
  parameter count `63,985`.
- Key metrics (single-seed smoke, not performance evidence):
  `rcc_full` train/unseen task return `-21.2942/-21.6299`,
  `rcc_no_task_commitment` `-25.1291/-25.1304`,
  `rcc_no_counterfactual` `-21.2942/-21.6299`, and
  `rcc_no_projection` `-21.2942/-21.6299`; all task-success rates were
  `0.0`, all hard-violation rates were `0.0` in both splits. Task-commitment
  action alignment was `0.3119/0.1871` for full and no-counterfactual/no-
  projection, and `0.0/0.0` for no-task-commitment.

### Active-task MAPPO conditioning controls

- Command: `python run_active_task_baselines.py --methods mappo_zero_context mappo_rule_vector mappo_rule_graph --seeds 11 --updates 1 --episodes 1 --horizon 4 --aircraft 2 --task interception --ppo-epoch 1 --hidden 32 --output results/next_step_baselines`
- Exit status: `0`.
- Result paths: `results/next_step_baselines/summary.json`,
  `per_seed.json`, `per_episode.json`, `training_trace.json`, and
  `control_audit.json`.
- Fixed variables: interception task, seed `11`, 2 aircraft, horizon `4`,
  one update, one evaluation episode, one PPO epoch, hidden width `32`;
  expected training budget is `4` environment steps per method.
- Control audit: `passed=true`; all methods observed `4` steps and parameter
  count `20,120`. Wrapper audit confirms
  `ZeroRuleVectorActiveTaskEnv`, `RuleVectorActiveTaskEnv`, and
  `RuleGraphActiveTaskEnv`; all context widths are `59`, zero-context L1 is
  `0.0`, and vector/graph contexts have positive L1.
- Key metrics: task return means were `-22.5573` (zero), `-22.5647`
  (vector), and `-22.5588` (graph); all success rates `0.0`, hard-violation
  rates `0.0`, and soft-violation rates `1.0`.

## Cross-artifact checks

- `results/next_step_ablations/control_audit.json`: `passed=true`; all four
  variants used 4 training environment steps and 63,985 parameters.
- `results/next_step_baselines/control_audit.json`: `passed=true`; all three
  MAPPO conditioning controls used 4 training environment steps and 20,120
  parameters. Context width was 59 for all controls; zero/vector/graph context
  norms were audited as 0/positive/positive.
- The manifests record the same interception task, paired scenario seed
  formulas, horizon 4, semantic action set, and one-update budget for the
  smoke runs. Exact parameter matching is claimed only within the registered
  conditioning controls and RCC ablations.
- `run_rcc_mechanism_evaluation.py` reports four unique nominal joint actions,
  composition sensitivity 1.0, and priority sensitivity 1.0. Its controller
  has no checkpoint, so this is evaluation-path validation rather than learned
  performance evidence.

## Limitations

- All runs above are minimal smoke/protocol runs with one seed and one update
  (or an untrained evaluation controller). They must not be reported as final
  superiority results. The next paper-grade run remains a registered
  multi-seed, longer-budget experiment.

## Additional pilot execution

- A longer pilot was started with 3 seeds, 20 updates and 30-step horizons for
  `rcc_full` versus `rcc_no_task_commitment`. The runner completed checkpoints
  for all three `rcc_full` seeds and one `rcc_no_task_commitment` seed, but did
  not emit aggregate summaries within a reasonable runtime. It was stopped
  intentionally. See `results/formal_pilot_interception_3seed20/INTERRUPTED.md`.
- No metric from this partial run is used as evidence.

## Engineering fixes after the protocol run

- Added `pythonpath = .` to `pytest.ini`; both `pytest -q` and
  `python -m pytest -q` now pass 125 tests.
- Changed RCC and active-task baseline checkpoint writes to atomic replacement.
  A two-step RCC smoke run produced a non-empty checkpoint and passed its
  control audit. This prevents interrupted runs from leaving misleading
  zero-byte checkpoint files.
