# Rule-Agent Dependency Graph

The online safety layer represents active knowledge as a bipartite graph:

- agent nodes are the aircraft whose actions may be changed;
- rule nodes are active or violated temporal requirements;
- an edge means that the agent's action affects the rule;
- local keys such as `I02:0` connect one agent;
- relational keys such as `S02:0-1` connect both agents;
- team rules such as `C02` connect all active agents.

Arbitration follows the hierarchy in `note1.md`:

1. physical and fault safety;
2. information and authorization;
3. coordination;
4. mission continuity;
5. efficiency preferences.

The dynamic priority also increases with predicted violation probability and
the number of affected agents. Hard rules cannot be relaxed. When hard and
soft rules cannot both be met, the lower-priority soft rule is recorded as
relaxed. Continuous residuals are then solved jointly by the existing SLSQP
layer.

Each `QPResidualSolution` now exposes:

- `dependency_graph`;
- `agent_rule_conflicts`;
- `conflict_events`;
- involved agents and rules;
- candidate resolution types;
- selected actions and per-agent residuals;
- relaxed rules;
- resolution status and reason.

The targeted experiment is `run_conflict_arbitration_experiments.py`. It
compares unshielded decisions, independent local filtering, heuristic joint
filtering, and dependency-graph QP arbitration on the five core templates
from `note1.md` plus three representative extensions from `note2.md`:
lost-link/intent sharing, capability loss/minimum dwell, and risk-budget/task
continuity.
