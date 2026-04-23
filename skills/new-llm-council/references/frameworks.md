# Decision framework catalogue (for LLM-Council-Decide)

When the user chooses the **Decide** base, they may hand-pick which frameworks go on the panel. Up to 5 frameworks per run — enough to triangulate, not so many the dossier becomes noise.

| # | Framework | Key | Scope |
|---|---|---|---|
| 1 | Pros & Cons | `pros_cons` | Baseline exhaustive listing with certainty markers and magnitude ranking |
| 2 | Weighted Decision Matrix | `weighted_matrix` | Quantitative — criteria, weights, option scores, sensitivity analysis |
| 3 | Expected Value | `expected_value` | Probability × payoff across scenarios, variance and tail-risk |
| 4 | 10/10/10 Rule (Welch) | `ten_ten_ten` | Temporal — consequences at 10 min / 10 months / 10 years |
| 5 | Regret Minimization (Bezos) | `regret_min` | View from 80: which choice will you regret less? |
| 6 | Type-1 / Type-2 Doors (Bezos) | `door_type` | Reversibility classifier — how much analysis does this deserve? |
| 7 | Pre-Mortem / Inversion | `pre_mortem` | Imagine the decision failed — work backward to causes |
| 8 | Second-Order Thinking (Marks) | `second_order` | Chain "and then what?" at least twice |
| 9 | OODA Loop (Boyd) | `ooda` | Observe-Orient-Decide-Act under time pressure |
| 10 | Cynefin (Snowden) | `cynefin` | Classify situation and match decision style |
| 11 | Kepner-Tregoe | `kepner_tregoe` | Musts (binary) vs Wants (scored) plus risk analysis |
| 12 | SWOT | `swot` | Strengths/Weaknesses × Opportunities/Threats |
| 13 | Six Thinking Hats (de Bono) | `six_hats` | Facts, feelings, caution, optimism, creativity, process |
| 14 | Munger Latticework | `munger` | Apply multiple disciplinary lenses |
| 15 | WRAP (Heath) | `wrap` | Widen options, Reality-test, Attain distance, Prepare to be wrong |

## Selection guidance

When helping the user pick, aim for **diversity of lens**:

- Include at least one **failure-first** framework (`pre_mortem`, `second_order`) if the decision is hard-to-reverse.
- Include at least one **quantitative** (`weighted_matrix`, `expected_value`) if options are comparable on measurable criteria.
- Include at least one **temporal / distance** framework (`ten_ten_ten`, `regret_min`) if the decision is emotionally loaded.
- Avoid stacking multiple frameworks that would all agree (e.g. Pros/Cons + SWOT + Six Hats are all "list things" — pick one).
- If the decision is low-stakes and reversible (`door_type` Type-2), use fewer frameworks (2–3).
