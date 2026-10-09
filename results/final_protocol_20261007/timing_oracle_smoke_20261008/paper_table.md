# Intervention timing (fixed nominal policy)

All endpoints use 30 steps from the same offline warning, including the unshielded delay.

| Distance | Timing | Method | N | Safe 3 | Safe 30 | Min separation m | C03 violation | Support service | Reward | QP fallback |
|---:|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 2000 | first_S02_violation | DG-QP | 1 | 0.000 | 0.000 | 229.630 | 0.100 | 0.900 | 10.330 | 0.100 |
| 2000 | first_S02_violation | JointHeuristic | 1 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.640 | 0.000 |
| 2000 | first_S02_violation | NoShield | 1 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | first_S02_violation | PartialShield | 1 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.885 | 0.000 |
| 2000 | warning_now | DG-QP | 1 | 1.000 | 0.000 | 663.106 | 0.000 | 1.000 | 10.329 | 0.067 |
| 2000 | warning_now | JointHeuristic | 1 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.640 | 0.000 |
| 2000 | warning_now | NoShield | 1 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_now | PartialShield | 1 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.885 | 0.000 |
| 2000 | warning_plus_1 | DG-QP | 1 | 0.000 | 0.000 | 351.058 | 0.033 | 0.967 | 9.625 | 0.167 |
| 2000 | warning_plus_1 | JointHeuristic | 1 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.640 | 0.000 |
| 2000 | warning_plus_1 | NoShield | 1 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_plus_1 | PartialShield | 1 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.885 | 0.000 |
| 2000 | warning_plus_2 | DG-QP | 1 | 0.000 | 0.000 | 134.097 | 0.067 | 0.933 | 9.493 | 0.133 |
| 2000 | warning_plus_2 | JointHeuristic | 1 | 0.000 | 0.000 | 230.069 | 1.000 | 0.000 | 25.640 | 0.000 |
| 2000 | warning_plus_2 | NoShield | 1 | 0.000 | 0.000 | 219.370 | 1.000 | 0.000 | 25.427 | 0.000 |
| 2000 | warning_plus_2 | PartialShield | 1 | 0.000 | 0.000 | 224.877 | 1.000 | 0.000 | 23.885 | 0.000 |
| 2400 | first_S02_violation | DG-QP | 1 | 1.000 | 0.000 | 206.042 | 0.133 | 0.867 | 10.949 | 0.100 |
| 2400 | first_S02_violation | JointHeuristic | 1 | 1.000 | 0.000 | 205.245 | 1.000 | 0.000 | 25.759 | 0.000 |
| 2400 | first_S02_violation | NoShield | 1 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | first_S02_violation | PartialShield | 1 | 1.000 | 0.000 | 201.329 | 1.000 | 0.000 | 24.024 | 0.000 |
| 2400 | warning_now | DG-QP | 1 | 1.000 | 0.000 | 688.066 | 0.000 | 1.000 | 10.360 | 0.100 |
| 2400 | warning_now | JointHeuristic | 1 | 1.000 | 0.000 | 226.344 | 1.000 | 0.000 | 25.696 | 0.000 |
| 2400 | warning_now | NoShield | 1 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_now | PartialShield | 1 | 1.000 | 0.000 | 201.329 | 1.000 | 0.000 | 24.024 | 0.000 |
| 2400 | warning_plus_1 | DG-QP | 1 | 1.000 | 0.000 | 515.744 | 0.033 | 0.967 | 10.355 | 0.200 |
| 2400 | warning_plus_1 | JointHeuristic | 1 | 1.000 | 0.000 | 226.344 | 1.000 | 0.000 | 25.696 | 0.000 |
| 2400 | warning_plus_1 | NoShield | 1 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_plus_1 | PartialShield | 1 | 1.000 | 0.000 | 201.329 | 1.000 | 0.000 | 24.024 | 0.000 |
| 2400 | warning_plus_2 | DG-QP | 1 | 1.000 | 0.000 | 368.348 | 0.067 | 0.933 | 10.170 | 0.167 |
| 2400 | warning_plus_2 | JointHeuristic | 1 | 1.000 | 0.000 | 226.344 | 1.000 | 0.000 | 25.696 | 0.000 |
| 2400 | warning_plus_2 | NoShield | 1 | 1.000 | 0.000 | 201.827 | 1.000 | 0.000 | 25.498 | 0.000 |
| 2400 | warning_plus_2 | PartialShield | 1 | 1.000 | 0.000 | 201.329 | 1.000 | 0.000 | 24.024 | 0.000 |

# Truth-informed recovery reference

| Distance | N | Grid recovered by 3 | Reference recovered by 3 | Reference min separation m | One-step outer distance bound m |
|---:|---:|---:|---:|---:|---:|
| 2000 | 1 | 1.000 | 1.000 | 303.204 | 312.147 |
| 2400 | 1 | 1.000 | 1.000 | 296.391 | 308.679 |

The reference is a validated feasible witness, not a globally optimal or deployable competitor. Recovery does not erase intermediate separation breaches.
Means aggregate episodes within seed first. Zero-jitter seeds are not independent geometries; varied cases are a separate protocol.
