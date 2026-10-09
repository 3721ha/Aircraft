# Method information

- Method name: HAPPO (Heterogeneous-Agent Proximal Policy Optimisation)
- Paper title: Trust Region Policy Optimisation in Multi-Agent Reinforcement Learning
- Paper URL: https://arxiv.org/abs/2109.11251
- Official repository URL: https://github.com/marlbenchmark/on-policy
- Commit: `de66d7a4b23fac2513f56f96f73b3f5cb96695ac`
- Local source: `../mappo/SOURCE/onpolicy/algorithms/happo` (the source is not duplicated)
- Local acquisition date: 2026-09-02
- License: MIT
- Third-party source modified: no
- Official implementation: `onpolicy/algorithms/happo/`
- Aircraft adapter: `external_adapters/official_happo.py`
- Aircraft experiment entry: `run_official_happo.py`
- Aircraft observation: separate local actor observations and concatenated centralized critic observations
- Aircraft action: shared five-dimensional continuous latent adapter
- Safety constraint: none; HAPPO is the heterogeneous nominal MARL comparison
- Core mechanism preserved: separate actor/critic pairs, randomized agent update order and multiplicative importance factor
- Adaptation limit: semantic mode and target are rounded at the simulator boundary
