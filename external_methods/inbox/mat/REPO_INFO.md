# Method information

- Method name: MAT (Multi-Agent Transformer)
- Paper title: Multi-Agent Reinforcement Learning is a Sequence Modeling Problem
- Year and venue: NeurIPS 2022
- Paper URL: https://arxiv.org/abs/2205.14953
- Official repository URL: https://github.com/PKU-MARL/Multi-Agent-Transformer
- Commit: `be3ff49c8264d454c1fe2c41582aa2bfc98498c8`
- Local acquisition date: 2026-09-02
- License: no LICENSE file is present at the pinned commit; redistribution permission is not established
- Third-party source modified: no
- Official implementation: `mat/algorithms/mat/`
- Aircraft adapter: `external_adapters/official_mat.py`
- Aircraft experiment entry: `run_official_mat.py`
- Aircraft action: shared five-dimensional continuous latent adapter
- Core mechanism preserved: Transformer encoder-decoder and autoregressive joint-action generation
- Execution information: all agents' local observations are assembled centrally to generate one joint action
- Fairness limitation: MAT therefore has stronger execution-time information than decentralized MAPPO/MACPO/HAPPO actors; report it as a centralized-communication baseline, not an equal-information baseline
- Safety constraint: none
- Dependency note: the adapter imports the official algorithm core under the current PyTorch environment and does not install the obsolete full benchmark stack
