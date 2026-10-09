# Method information

- Method name: HATRPO (Heterogeneous-Agent Trust Region Policy Optimisation)
- Paper title: Trust Region Policy Optimisation in Multi-Agent Reinforcement Learning
- Year and venue: ICLR 2022
- Paper URL: https://arxiv.org/abs/2109.11251
- Official repository URL: https://github.com/marlbenchmark/on-policy
- Commit: `de66d7a4b23fac2513f56f96f73b3f5cb96695ac`
- Local source: `../mappo/SOURCE/onpolicy/algorithms/hatrpo` (the source is not duplicated)
- License: MIT
- Third-party source modified: no
- Aircraft adapter: `external_adapters/official_hatrpo.py`
- Aircraft experiment entry: `run_official_hatrpo.py`
- Aircraft action: shared five-dimensional continuous latent adapter
- Core mechanism preserved: separate policies, randomized sequential updates, conjugate gradient, KL trust region and backtracking line search
- Compatibility shim: upstream passes an always-None availability argument to the continuous Gaussian forward method; the adapter accepts and ignores only that argument
- Safety constraint: none; HATRPO is a trust-region nominal MARL baseline
