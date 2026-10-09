# Actual post-violation recovery (paired takeover)

k=0 is an observed violation. k=1..3 are three executed actions after takeover. All methods clone the same trigger state.

| Initial distance (m) | Method | Triggered episodes | Recovered by 3 | Confirmed by 3 | Recovered by 3, held to 30 | Min separation after takeover (m) | QP fallback |
|---:|---|---:|---:|---:|---:|---:|---:|
| 2000 | NoShield | 10 | 0.000 | 0.000 | 0.000 | 219.370 | 0.000 |
| 2000 | PartialShield | 10 | 0.000 | 0.000 | 0.000 | 224.877 | 0.000 |
| 2000 | JointHeuristic | 10 | 0.000 | 0.000 | 0.000 | 230.069 | 0.000 |
| 2000 | DG-QP | 10 | 0.000 | 0.000 | 0.000 | 229.630 | 0.100 |
| 2200 | NoShield | 10 | 1.000 | 0.000 | 1.000 | 164.587 | 0.000 |
| 2200 | PartialShield | 10 | 1.000 | 0.000 | 1.000 | 151.483 | 0.000 |
| 2200 | JointHeuristic | 10 | 1.000 | 0.000 | 1.000 | 148.476 | 0.000 |
| 2200 | DG-QP | 10 | 1.000 | 0.000 | 1.000 | 147.012 | 0.067 |
| 2400 | NoShield | 10 | 1.000 | 0.000 | 1.000 | 201.827 | 0.000 |
| 2400 | PartialShield | 10 | 0.000 | 0.000 | 0.000 | 201.348 | 0.000 |
| 2400 | JointHeuristic | 10 | 0.000 | 0.000 | 0.000 | 204.863 | 0.000 |
| 2400 | DG-QP | 10 | 0.000 | 0.000 | 0.000 | 206.042 | 0.100 |
| 2800 | NoShield | 10 | 1.000 | 0.000 | 1.000 | 223.568 | 0.000 |
| 2800 | PartialShield | 10 | 1.000 | 0.000 | 1.000 | 216.686 | 0.000 |
| 2800 | JointHeuristic | 10 | 0.300 | 0.000 | 0.300 | 217.998 | 0.000 |
| 2800 | DG-QP | 10 | 1.000 | 0.000 | 1.000 | 218.345 | 0.100 |
| 3200 | NoShield | 10 | 1.000 | 0.000 | 1.000 | 285.176 | 0.000 |
| 3200 | PartialShield | 10 | 1.000 | 0.000 | 1.000 | 275.266 | 0.000 |
| 3200 | JointHeuristic | 10 | 1.000 | 0.000 | 1.000 | 274.314 | 0.000 |
| 3200 | DG-QP | 10 | 1.000 | 0.000 | 1.000 | 272.990 | 0.067 |

A failed trigger is excluded from all methods together and remains in triggers.json. No post-trigger feasibility filtering is applied.
Recovery can result from aircraft passing each other after a deep separation breach. Consult the minimum separation and full trace; this endpoint alone does not demonstrate collision avoidance.
Rows are shield configurations over the same fixed nominal policy, not seven learned algorithms.
