# Intervention timing (fixed nominal policy)

All endpoints use 30 steps from the same offline warning, including the unshielded delay.

| Distance | Timing | Method | N | Safe 3 | Safe 30 | Min separation m | C03 violation | Support service | Reward | QP fallback |
|---:|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 2000 | first_S02_violation | DG-QP | 10 | 0.000 | 0.000 | 229.630 | 0.100 | 0.900 | 10.330 | 0.100 |
| 2000 | first_S02_violation | JointHeuristic | 10 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.622 | 0.000 |
| 2000 | first_S02_violation | NoShield | 10 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | first_S02_violation | PartialShield | 10 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.443 | 0.000 |
| 2000 | warning_now | DG-QP | 10 | 1.000 | 0.000 | 663.106 | 0.000 | 1.000 | 10.329 | 0.067 |
| 2000 | warning_now | JointHeuristic | 10 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.622 | 0.000 |
| 2000 | warning_now | NoShield | 10 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_now | PartialShield | 10 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.443 | 0.000 |
| 2000 | warning_plus_1 | DG-QP | 10 | 0.000 | 0.000 | 351.058 | 0.033 | 0.967 | 9.625 | 0.167 |
| 2000 | warning_plus_1 | JointHeuristic | 10 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.622 | 0.000 |
| 2000 | warning_plus_1 | NoShield | 10 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_plus_1 | PartialShield | 10 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.443 | 0.000 |
| 2000 | warning_plus_2 | DG-QP | 10 | 0.000 | 0.000 | 134.097 | 0.067 | 0.933 | 9.493 | 0.133 |
| 2000 | warning_plus_2 | JointHeuristic | 10 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.622 | 0.000 |
| 2000 | warning_plus_2 | NoShield | 10 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_plus_2 | PartialShield | 10 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.443 | 0.000 |
| 2200 | first_S02_violation | DG-QP | 10 | 1.000 | 0.000 | 147.012 | 0.133 | 0.867 | 11.013 | 0.067 |
| 2200 | first_S02_violation | JointHeuristic | 10 | 1.000 | 0.000 | 148.476 | 1.000 | 0.000 | 25.694 | 0.000 |
| 2200 | first_S02_violation | NoShield | 10 | 1.000 | 0.000 | 164.587 | 1.000 | 0.000 | 25.430 | 0.000 |
| 2200 | first_S02_violation | PartialShield | 10 | 1.000 | 0.000 | 151.483 | 1.000 | 0.000 | 24.025 | 0.000 |
| 2200 | warning_now | DG-QP | 10 | 1.000 | 0.000 | 545.595 | 0.000 | 1.000 | 9.849 | 0.100 |
| 2200 | warning_now | JointHeuristic | 10 | 1.000 | 0.000 | 116.882 | 1.000 | 0.000 | 25.643 | 0.000 |
| 2200 | warning_now | NoShield | 10 | 1.000 | 0.000 | 164.587 | 1.000 | 0.000 | 25.430 | 0.000 |
| 2200 | warning_now | PartialShield | 10 | 1.000 | 0.000 | 151.483 | 1.000 | 0.000 | 24.025 | 0.000 |
| 2200 | warning_plus_1 | DG-QP | 10 | 1.000 | 0.000 | 435.201 | 0.033 | 0.967 | 10.102 | 0.133 |
| 2200 | warning_plus_1 | JointHeuristic | 10 | 1.000 | 0.000 | 116.882 | 1.000 | 0.000 | 25.643 | 0.000 |
| 2200 | warning_plus_1 | NoShield | 10 | 1.000 | 0.000 | 164.587 | 1.000 | 0.000 | 25.430 | 0.000 |
| 2200 | warning_plus_1 | PartialShield | 10 | 1.000 | 0.000 | 151.483 | 1.000 | 0.000 | 24.025 | 0.000 |
| 2200 | warning_plus_2 | DG-QP | 10 | 1.000 | 0.000 | 262.843 | 0.067 | 0.933 | 10.111 | 0.133 |
| 2200 | warning_plus_2 | JointHeuristic | 10 | 1.000 | 0.000 | 116.882 | 1.000 | 0.000 | 25.643 | 0.000 |
| 2200 | warning_plus_2 | NoShield | 10 | 1.000 | 0.000 | 164.587 | 1.000 | 0.000 | 25.430 | 0.000 |
| 2200 | warning_plus_2 | PartialShield | 10 | 1.000 | 0.000 | 151.483 | 1.000 | 0.000 | 24.025 | 0.000 |
| 2400 | first_S02_violation | DG-QP | 10 | 1.000 | 0.000 | 206.042 | 0.133 | 0.867 | 10.949 | 0.100 |
| 2400 | first_S02_violation | JointHeuristic | 10 | 1.000 | 0.000 | 204.863 | 1.000 | 0.000 | 25.732 | 0.000 |
| 2400 | first_S02_violation | NoShield | 10 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | first_S02_violation | PartialShield | 10 | 1.000 | 0.000 | 201.348 | 1.000 | 0.000 | 23.561 | 0.000 |
| 2400 | warning_now | DG-QP | 10 | 1.000 | 0.000 | 688.066 | 0.000 | 1.000 | 10.360 | 0.100 |
| 2400 | warning_now | JointHeuristic | 10 | 1.000 | 0.000 | 224.814 | 1.000 | 0.000 | 25.649 | 0.000 |
| 2400 | warning_now | NoShield | 10 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_now | PartialShield | 10 | 1.000 | 0.000 | 201.348 | 1.000 | 0.000 | 23.561 | 0.000 |
| 2400 | warning_plus_1 | DG-QP | 10 | 1.000 | 0.000 | 515.744 | 0.033 | 0.967 | 10.355 | 0.200 |
| 2400 | warning_plus_1 | JointHeuristic | 10 | 1.000 | 0.000 | 224.814 | 1.000 | 0.000 | 25.649 | 0.000 |
| 2400 | warning_plus_1 | NoShield | 10 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_plus_1 | PartialShield | 10 | 1.000 | 0.000 | 201.348 | 1.000 | 0.000 | 23.561 | 0.000 |
| 2400 | warning_plus_2 | DG-QP | 10 | 1.000 | 0.000 | 368.348 | 0.067 | 0.933 | 10.170 | 0.167 |
| 2400 | warning_plus_2 | JointHeuristic | 10 | 1.000 | 0.000 | 224.814 | 1.000 | 0.000 | 25.649 | 0.000 |
| 2400 | warning_plus_2 | NoShield | 10 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_plus_2 | PartialShield | 10 | 1.000 | 0.000 | 201.348 | 1.000 | 0.000 | 23.561 | 0.000 |
| 2800 | first_S02_violation | DG-QP | 10 | 1.000 | 0.000 | 218.345 | 0.133 | 0.867 | 11.184 | 0.100 |
| 2800 | first_S02_violation | JointHeuristic | 10 | 1.000 | 0.000 | 217.998 | 1.000 | 0.000 | 25.860 | 0.000 |
| 2800 | first_S02_violation | NoShield | 10 | 1.000 | 0.000 | 223.568 | 1.000 | 0.000 | 25.586 | 0.000 |
| 2800 | first_S02_violation | PartialShield | 10 | 1.000 | 0.000 | 216.686 | 1.000 | 0.000 | 24.134 | 0.000 |
| 2800 | warning_now | DG-QP | 10 | 1.000 | 0.000 | 824.686 | 0.000 | 1.000 | 10.500 | 0.033 |
| 2800 | warning_now | JointHeuristic | 10 | 1.000 | 0.000 | 220.367 | 1.000 | 0.000 | 25.775 | 0.000 |
| 2800 | warning_now | NoShield | 10 | 1.000 | 0.000 | 223.568 | 1.000 | 0.000 | 25.586 | 0.000 |
| 2800 | warning_now | PartialShield | 10 | 1.000 | 0.000 | 216.686 | 1.000 | 0.000 | 24.134 | 0.000 |
| 2800 | warning_plus_1 | DG-QP | 10 | 1.000 | 0.000 | 504.349 | 0.033 | 0.967 | 10.332 | 0.167 |
| 2800 | warning_plus_1 | JointHeuristic | 10 | 1.000 | 0.000 | 220.367 | 1.000 | 0.000 | 25.775 | 0.000 |
| 2800 | warning_plus_1 | NoShield | 10 | 1.000 | 0.000 | 223.568 | 1.000 | 0.000 | 25.586 | 0.000 |
| 2800 | warning_plus_1 | PartialShield | 10 | 1.000 | 0.000 | 216.686 | 1.000 | 0.000 | 24.134 | 0.000 |
| 2800 | warning_plus_2 | DG-QP | 10 | 1.000 | 0.000 | 357.983 | 0.067 | 0.933 | 10.261 | 0.167 |
| 2800 | warning_plus_2 | JointHeuristic | 10 | 1.000 | 0.000 | 220.367 | 1.000 | 0.000 | 25.775 | 0.000 |
| 2800 | warning_plus_2 | NoShield | 10 | 1.000 | 0.000 | 223.568 | 1.000 | 0.000 | 25.586 | 0.000 |
| 2800 | warning_plus_2 | PartialShield | 10 | 1.000 | 0.000 | 216.686 | 1.000 | 0.000 | 24.134 | 0.000 |
| 3200 | first_S02_violation | DG-QP | 10 | 1.000 | 0.000 | 272.990 | 0.133 | 0.867 | 11.336 | 0.067 |
| 3200 | first_S02_violation | JointHeuristic | 10 | 1.000 | 0.000 | 274.314 | 1.000 | 0.000 | 26.034 | 0.000 |
| 3200 | first_S02_violation | NoShield | 10 | 1.000 | 0.000 | 285.176 | 1.000 | 0.000 | 25.747 | 0.000 |
| 3200 | first_S02_violation | PartialShield | 10 | 1.000 | 0.000 | 275.266 | 1.000 | 0.000 | 24.293 | 0.000 |
| 3200 | warning_now | DG-QP | 10 | 1.000 | 0.000 | 585.314 | 0.000 | 1.000 | 9.994 | 0.100 |
| 3200 | warning_now | JointHeuristic | 10 | 1.000 | 0.000 | 255.468 | 1.000 | 0.000 | 26.008 | 0.000 |
| 3200 | warning_now | NoShield | 10 | 1.000 | 0.000 | 285.176 | 1.000 | 0.000 | 25.747 | 0.000 |
| 3200 | warning_now | PartialShield | 10 | 1.000 | 0.000 | 275.266 | 1.000 | 0.000 | 24.293 | 0.000 |
| 3200 | warning_plus_1 | DG-QP | 10 | 1.000 | 0.000 | 500.760 | 0.033 | 0.967 | 10.327 | 0.100 |
| 3200 | warning_plus_1 | JointHeuristic | 10 | 1.000 | 0.000 | 255.468 | 1.000 | 0.000 | 26.008 | 0.000 |
| 3200 | warning_plus_1 | NoShield | 10 | 1.000 | 0.000 | 285.176 | 1.000 | 0.000 | 25.747 | 0.000 |
| 3200 | warning_plus_1 | PartialShield | 10 | 1.000 | 0.000 | 275.266 | 1.000 | 0.000 | 24.293 | 0.000 |
| 3200 | warning_plus_2 | DG-QP | 10 | 1.000 | 0.000 | 363.421 | 0.067 | 0.933 | 10.409 | 0.100 |
| 3200 | warning_plus_2 | JointHeuristic | 10 | 1.000 | 0.000 | 255.468 | 1.000 | 0.000 | 26.008 | 0.000 |
| 3200 | warning_plus_2 | NoShield | 10 | 1.000 | 0.000 | 285.176 | 1.000 | 0.000 | 25.747 | 0.000 |
| 3200 | warning_plus_2 | PartialShield | 10 | 1.000 | 0.000 | 275.266 | 1.000 | 0.000 | 24.293 | 0.000 |

# Truth-informed recovery reference

| Distance | N | Grid recovered by 3 | Reference recovered by 3 | Reference min separation m | One-step outer distance bound m |
|---:|---:|---:|---:|---:|---:|
| 2000 | 10 | 1.000 | 1.000 | 303.204 | 312.147 |
| 2200 | 10 | 1.000 | 1.000 | 256.932 | 264.413 |
| 2400 | 10 | 1.000 | 1.000 | 296.391 | 308.679 |
| 2800 | 10 | 1.000 | 1.000 | 319.574 | 333.438 |
| 3200 | 10 | 1.000 | 1.000 | 384.003 | 388.117 |

The reference is a validated feasible witness, not a globally optimal or deployable competitor. Recovery does not erase intermediate separation breaches.
Means aggregate episodes within seed first. Zero-jitter seeds are not independent geometries; varied cases are a separate protocol.
