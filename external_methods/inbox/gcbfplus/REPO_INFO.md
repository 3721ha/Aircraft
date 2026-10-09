# Method information

- Method name: GCBF+
- Paper title: GCBF+: A Neural Graph Control Barrier Function Framework for Distributed Safe Multi-Agent Control
- Year and venue: IEEE Transactions on Robotics, 2025, volume 41, pages 1533-1552
- DOI: 10.1109/TRO.2025.3530348
- Paper URL: https://arxiv.org/abs/2401.14554
- Official repository URL: https://github.com/MIT-REALM/gcbfplus
- Commit: `fb449907bdbf981aa10f0edfecca02663ddc8037`
- Local acquisition date: 2026-09-02
- License: MIT
- Third-party source modified: no
- Official training entry: `train.py --algo gcbf+`
- Official test entry: `test.py`
- Aircraft bridge: `external_adapters/official_gcbfplus.py`
- Aircraft experiment entry: `run_official_gcbfplus.py`
- Comparison scope: physical S01/S02/S03 rules only
- Adaptation: the nominal Aircraft policy retains semantic mode/target; GCBF+ replaces turn, climb and acceleration
- Obstacle mapping: the checkpoint was trained with 8 random obstacles, but Aircraft exposes no obstacle state; deployment therefore uses zero obstacle instances rather than injecting phantom hazards
- Pretrained model: official 8-agent LinearDrone checkpoint at step 1000; graph-equivariant parameters are deployed on 3 Aircraft agents
- Transfer limitation: the checkpoint was not trained with Aircraft dynamics, so this is an off-the-shelf transfer baseline rather than equal-domain training
- Reporting rule: do not compare its full-rule joint satisfaction against methods that model authorization, coordination and task-continuity rules
- Environment: use an isolated Python 3.10 environment because the main project uses Python 3.12/PyTorch and GCBF+ has a separate JAX stack

## Isolated environment

From the Aircraft project root:

```powershell
$env:UV_CACHE_DIR = "$PWD\.uv-cache"
uv venv --python 3.10 .venv-gcbf
uv pip install --python .venv-gcbf\Scripts\python.exe torch
uv pip install --python .venv-gcbf\Scripts\python.exe -r external_methods\inbox\gcbfplus\REQUIREMENTS_INFERENCE.txt
```

Dependency check:

```powershell
.venv-gcbf\Scripts\python.exe run_official_gcbfplus.py --check-only
```

The workspace-local `UV_CACHE_DIR` is required on machines where the default user cache is not writable. The
experiment reports the nominal policy, the internal physical CBF-QP reference, and official GCBF+ on identical
scenarios; only the S01/S02/S03 physical metrics are comparable.

If the full upstream requirements command is slow, cancel it and use the minimal inference file above. The
remaining `jaxproxqp` line is a GitHub-only dependency and may still be network-limited; install the PyPI portion
first, then retry that line separately if needed. The fastest split form is:

```powershell
$env:UV_CACHE_DIR = "$PWD\.uv-cache"
uv pip install --python .venv-gcbf\Scripts\python.exe -r external_methods\inbox\gcbfplus\REQUIREMENTS_INFERENCE_PYPI.txt
uv pip install --python .venv-gcbf\Scripts\python.exe "git+https://github.com/oswinso/jaxproxqp.git"
```
