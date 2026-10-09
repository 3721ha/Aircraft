# Intervention timing (fixed nominal policy)

All endpoints use 30 steps from the same offline warning, including the unshielded delay.

| Distance | Timing | Method | N | Safe 3 | Safe 30 | Min separation m | C03 violation | Support service | Reward | QP fallback |
|---:|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 2000 | first_S02_violation | DG-QP | 20 | 0.150 | 0.000 | 190.420 | 0.105 | 0.895 | 10.503 | 0.095 |
| 2000 | first_S02_violation | JointHeuristic | 20 | 0.150 | 0.000 | 191.909 | 1.000 | 0.000 | 25.693 | 0.000 |
| 2000 | first_S02_violation | NoShield | 20 | 0.150 | 0.000 | 194.751 | 1.000 | 0.000 | 25.426 | 0.000 |
| 2000 | first_S02_violation | PartialShield | 20 | 0.150 | 0.000 | 192.195 | 1.000 | 0.000 | 23.548 | 0.000 |
| 2000 | warning_now | DG-QP | 20 | 0.800 | 0.000 | 603.194 | 0.000 | 1.000 | 10.131 | 0.085 |
| 2000 | warning_now | JointHeuristic | 20 | 0.150 | 0.000 | 191.263 | 1.000 | 0.000 | 25.697 | 0.000 |
| 2000 | warning_now | NoShield | 20 | 0.150 | 0.000 | 194.751 | 1.000 | 0.000 | 25.426 | 0.000 |
| 2000 | warning_now | PartialShield | 20 | 0.150 | 0.000 | 192.195 | 1.000 | 0.000 | 23.548 | 0.000 |
| 2000 | warning_plus_1 | DG-QP | 20 | 0.250 | 0.000 | 378.606 | 0.033 | 0.967 | 9.816 | 0.148 |
| 2000 | warning_plus_1 | JointHeuristic | 20 | 0.150 | 0.000 | 191.263 | 1.000 | 0.000 | 25.697 | 0.000 |
| 2000 | warning_plus_1 | NoShield | 20 | 0.150 | 0.000 | 194.751 | 1.000 | 0.000 | 25.426 | 0.000 |
| 2000 | warning_plus_1 | PartialShield | 20 | 0.150 | 0.000 | 192.195 | 1.000 | 0.000 | 23.548 | 0.000 |
| 2000 | warning_plus_2 | DG-QP | 20 | 0.150 | 0.000 | 163.222 | 0.067 | 0.933 | 9.618 | 0.155 |
| 2000 | warning_plus_2 | JointHeuristic | 20 | 0.150 | 0.000 | 191.263 | 1.000 | 0.000 | 25.697 | 0.000 |
| 2000 | warning_plus_2 | NoShield | 20 | 0.150 | 0.000 | 194.751 | 1.000 | 0.000 | 25.426 | 0.000 |
| 2000 | warning_plus_2 | PartialShield | 20 | 0.150 | 0.000 | 192.195 | 1.000 | 0.000 | 23.548 | 0.000 |
| 2200 | first_S02_violation | DG-QP | 20 | 0.700 | 0.000 | 184.689 | 0.123 | 0.877 | 10.929 | 0.087 |
| 2200 | first_S02_violation | JointHeuristic | 20 | 0.700 | 0.000 | 187.911 | 1.000 | 0.000 | 25.796 | 0.000 |
| 2200 | first_S02_violation | NoShield | 20 | 0.700 | 0.000 | 213.167 | 1.000 | 0.000 | 25.521 | 0.000 |
| 2200 | first_S02_violation | PartialShield | 20 | 0.700 | 0.000 | 193.636 | 1.000 | 0.000 | 23.913 | 0.000 |
| 2200 | warning_now | DG-QP | 20 | 1.000 | 0.000 | 596.567 | 0.000 | 1.000 | 10.043 | 0.087 |
| 2200 | warning_now | JointHeuristic | 20 | 0.700 | 0.000 | 178.062 | 1.000 | 0.000 | 25.772 | 0.000 |
| 2200 | warning_now | NoShield | 20 | 0.700 | 0.000 | 213.167 | 1.000 | 0.000 | 25.521 | 0.000 |
| 2200 | warning_now | PartialShield | 20 | 0.700 | 0.000 | 193.636 | 1.000 | 0.000 | 23.913 | 0.000 |
| 2200 | warning_plus_1 | DG-QP | 20 | 1.000 | 0.000 | 486.565 | 0.033 | 0.967 | 10.279 | 0.125 |
| 2200 | warning_plus_1 | JointHeuristic | 20 | 0.700 | 0.000 | 178.062 | 1.000 | 0.000 | 25.772 | 0.000 |
| 2200 | warning_plus_1 | NoShield | 20 | 0.700 | 0.000 | 213.167 | 1.000 | 0.000 | 25.521 | 0.000 |
| 2200 | warning_plus_1 | PartialShield | 20 | 0.700 | 0.000 | 193.636 | 1.000 | 0.000 | 23.913 | 0.000 |
| 2200 | warning_plus_2 | DG-QP | 20 | 0.850 | 0.000 | 292.160 | 0.067 | 0.933 | 10.137 | 0.147 |
| 2200 | warning_plus_2 | JointHeuristic | 20 | 0.700 | 0.000 | 178.062 | 1.000 | 0.000 | 25.772 | 0.000 |
| 2200 | warning_plus_2 | NoShield | 20 | 0.700 | 0.000 | 213.167 | 1.000 | 0.000 | 25.521 | 0.000 |
| 2200 | warning_plus_2 | PartialShield | 20 | 0.700 | 0.000 | 193.636 | 1.000 | 0.000 | 23.913 | 0.000 |
| 2400 | first_S02_violation | DG-QP | 20 | 1.000 | 0.000 | 178.516 | 0.133 | 0.867 | 10.955 | 0.097 |
| 2400 | first_S02_violation | JointHeuristic | 20 | 1.000 | 0.000 | 178.015 | 1.000 | 0.000 | 25.712 | 0.000 |
| 2400 | first_S02_violation | NoShield | 20 | 1.000 | 0.000 | 179.666 | 1.000 | 0.000 | 25.457 | 0.000 |
| 2400 | first_S02_violation | PartialShield | 20 | 1.000 | 0.000 | 176.512 | 1.000 | 0.000 | 23.835 | 0.000 |
| 2400 | warning_now | DG-QP | 20 | 1.000 | 0.000 | 647.576 | 0.000 | 1.000 | 10.160 | 0.092 |
| 2400 | warning_now | JointHeuristic | 20 | 1.000 | 0.000 | 186.583 | 1.000 | 0.000 | 25.701 | 0.000 |
| 2400 | warning_now | NoShield | 20 | 1.000 | 0.000 | 179.666 | 1.000 | 0.000 | 25.457 | 0.000 |
| 2400 | warning_now | PartialShield | 20 | 1.000 | 0.000 | 176.512 | 1.000 | 0.000 | 23.835 | 0.000 |
| 2400 | warning_plus_1 | DG-QP | 20 | 1.000 | 0.000 | 539.279 | 0.033 | 0.967 | 10.418 | 0.117 |
| 2400 | warning_plus_1 | JointHeuristic | 20 | 1.000 | 0.000 | 186.583 | 1.000 | 0.000 | 25.701 | 0.000 |
| 2400 | warning_plus_1 | NoShield | 20 | 1.000 | 0.000 | 179.666 | 1.000 | 0.000 | 25.457 | 0.000 |
| 2400 | warning_plus_1 | PartialShield | 20 | 1.000 | 0.000 | 176.512 | 1.000 | 0.000 | 23.835 | 0.000 |
| 2400 | warning_plus_2 | DG-QP | 20 | 1.000 | 0.000 | 340.096 | 0.067 | 0.933 | 10.159 | 0.152 |
| 2400 | warning_plus_2 | JointHeuristic | 20 | 1.000 | 0.000 | 186.583 | 1.000 | 0.000 | 25.701 | 0.000 |
| 2400 | warning_plus_2 | NoShield | 20 | 1.000 | 0.000 | 179.666 | 1.000 | 0.000 | 25.457 | 0.000 |
| 2400 | warning_plus_2 | PartialShield | 20 | 1.000 | 0.000 | 176.512 | 1.000 | 0.000 | 23.835 | 0.000 |
| 2800 | first_S02_violation | DG-QP | 20 | 1.000 | 0.000 | 231.847 | 0.133 | 0.867 | 11.247 | 0.083 |
| 2800 | first_S02_violation | JointHeuristic | 20 | 1.000 | 0.000 | 231.726 | 1.000 | 0.000 | 25.895 | 0.000 |
| 2800 | first_S02_violation | NoShield | 20 | 1.000 | 0.000 | 236.143 | 1.000 | 0.000 | 25.621 | 0.000 |
| 2800 | first_S02_violation | PartialShield | 20 | 1.000 | 0.000 | 230.235 | 1.000 | 0.000 | 24.119 | 0.000 |
| 2800 | warning_now | DG-QP | 20 | 1.000 | 0.000 | 676.226 | 0.000 | 1.000 | 10.274 | 0.072 |
| 2800 | warning_now | JointHeuristic | 20 | 1.000 | 0.000 | 231.466 | 1.000 | 0.000 | 25.850 | 0.000 |
| 2800 | warning_now | NoShield | 20 | 1.000 | 0.000 | 236.143 | 1.000 | 0.000 | 25.621 | 0.000 |
| 2800 | warning_now | PartialShield | 20 | 1.000 | 0.000 | 230.235 | 1.000 | 0.000 | 24.119 | 0.000 |
| 2800 | warning_plus_1 | DG-QP | 20 | 1.000 | 0.000 | 554.325 | 0.033 | 0.967 | 10.541 | 0.120 |
| 2800 | warning_plus_1 | JointHeuristic | 20 | 1.000 | 0.000 | 231.466 | 1.000 | 0.000 | 25.850 | 0.000 |
| 2800 | warning_plus_1 | NoShield | 20 | 1.000 | 0.000 | 236.143 | 1.000 | 0.000 | 25.621 | 0.000 |
| 2800 | warning_plus_1 | PartialShield | 20 | 1.000 | 0.000 | 230.235 | 1.000 | 0.000 | 24.119 | 0.000 |
| 2800 | warning_plus_2 | DG-QP | 20 | 1.000 | 0.000 | 375.207 | 0.067 | 0.933 | 10.413 | 0.150 |
| 2800 | warning_plus_2 | JointHeuristic | 20 | 1.000 | 0.000 | 231.466 | 1.000 | 0.000 | 25.850 | 0.000 |
| 2800 | warning_plus_2 | NoShield | 20 | 1.000 | 0.000 | 236.143 | 1.000 | 0.000 | 25.621 | 0.000 |
| 2800 | warning_plus_2 | PartialShield | 20 | 1.000 | 0.000 | 230.235 | 1.000 | 0.000 | 24.119 | 0.000 |
| 3200 | first_S02_violation | DG-QP | 20 | 1.000 | 0.000 | 266.797 | 0.135 | 0.865 | 11.393 | 0.075 |
| 3200 | first_S02_violation | JointHeuristic | 20 | 1.000 | 0.000 | 267.387 | 1.000 | 0.000 | 26.046 | 0.000 |
| 3200 | first_S02_violation | NoShield | 20 | 1.000 | 0.000 | 282.653 | 1.000 | 0.000 | 25.735 | 0.000 |
| 3200 | first_S02_violation | PartialShield | 20 | 1.000 | 0.000 | 268.961 | 1.000 | 0.000 | 24.198 | 0.000 |
| 3200 | warning_now | DG-QP | 20 | 1.000 | 0.000 | 625.618 | 0.000 | 1.000 | 10.180 | 0.080 |
| 3200 | warning_now | JointHeuristic | 20 | 1.000 | 0.000 | 253.963 | 1.000 | 0.000 | 26.016 | 0.000 |
| 3200 | warning_now | NoShield | 20 | 1.000 | 0.000 | 282.653 | 1.000 | 0.000 | 25.735 | 0.000 |
| 3200 | warning_now | PartialShield | 20 | 1.000 | 0.000 | 268.961 | 1.000 | 0.000 | 24.198 | 0.000 |
| 3200 | warning_plus_1 | DG-QP | 20 | 1.000 | 0.000 | 541.879 | 0.033 | 0.967 | 10.503 | 0.117 |
| 3200 | warning_plus_1 | JointHeuristic | 20 | 1.000 | 0.000 | 253.963 | 1.000 | 0.000 | 26.016 | 0.000 |
| 3200 | warning_plus_1 | NoShield | 20 | 1.000 | 0.000 | 282.653 | 1.000 | 0.000 | 25.735 | 0.000 |
| 3200 | warning_plus_1 | PartialShield | 20 | 1.000 | 0.000 | 268.961 | 1.000 | 0.000 | 24.198 | 0.000 |
| 3200 | warning_plus_2 | DG-QP | 20 | 1.000 | 0.000 | 391.984 | 0.067 | 0.933 | 10.545 | 0.143 |
| 3200 | warning_plus_2 | JointHeuristic | 20 | 1.000 | 0.000 | 253.963 | 1.000 | 0.000 | 26.016 | 0.000 |
| 3200 | warning_plus_2 | NoShield | 20 | 1.000 | 0.000 | 282.653 | 1.000 | 0.000 | 25.735 | 0.000 |
| 3200 | warning_plus_2 | PartialShield | 20 | 1.000 | 0.000 | 268.961 | 1.000 | 0.000 | 24.198 | 0.000 |

# Truth-informed recovery reference

| Distance | N | Grid recovered by 3 | Reference recovered by 3 | Reference min separation m | One-step outer distance bound m |
|---:|---:|---:|---:|---:|---:|
| 2000 | 20 | 1.000 | 1.000 | 284.246 | 294.192 |
| 2200 | 20 | 1.000 | 1.000 | 328.439 | 338.415 |
| 2400 | 20 | 1.000 | 1.000 | 273.551 | 284.226 |
| 2800 | 20 | 1.000 | 1.000 | 332.105 | 343.842 |
| 3200 | 20 | 1.000 | 1.000 | 384.594 | 393.725 |

The reference is a validated feasible witness, not a globally optimal or deployable competitor. Recovery does not erase intermediate separation breaches.
Means aggregate episodes within seed first. Zero-jitter seeds are not independent geometries; varied cases are a separate protocol.
