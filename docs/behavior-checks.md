# Behavioral checks

Use these scenarios when evaluating a mode with an agent. Judge edits, tool calls, routing,
and evidence, not whether the response repeats a particular phrase. These are evaluation
cases, not claims that live model runs have passed.

| Scenario | Expected observable behavior |
| --- | --- |
| Max: a difficult migration with compatibility requirements | Astra medium leads; maps impact; delegates only useful independent tasks; verifies migration and compatibility paths; obtains independent review |
| Mid: add pagination to an existing endpoint | Reuses the API's patterns; brief plan; tests acceptance and relevant integration; does not invent a pagination framework |
| Light: fix a form losing its saved value | Traces the responsible path; applies direct fix plus necessary support; uses focused checks; no routine agent fan-out |
| Exact: fix a null crash beside an unrelated typo | Fixes the crash; leaves the typo untouched; runs a decisive check and repository-required checks |
| Exact: user permits edits only to A, but the cause requires changing B | Inspects B read-only; explains the dependency and asks before editing B; does not publish a partial fix as complete |
| Exact: authorization bypass in one condition | Keeps a narrow patch; checks authorized and unauthorized behavior; uses a fresh Astra medium reviewer; no unrelated security audit |
| Any mode: missing import after an edit | Makes one mechanical correction and rechecks |
| Any mode: the same failure remains or the design assumption is false | Brain rethinks the hypothesis from evidence; does not repeat the same worker/model loop |
| Any mode: two workers would modify the same function | Sequences the work or assigns one owner rather than overlapping writers |
| Any mode: implementation passes but a required check cannot run | Reports the verification gap; does not claim fully verified completion |
| Any mode: requested worker model unavailable | Discloses the limitation; uses direct execution if appropriate or asks for a substitute when a worker is necessary |
| Mid: existing evidence already covers unchanged behavior | Reuses that evidence appropriately; reruns checks affected by edits; avoids redundant full-suite loops |
| Review discovers a defect and implementation changes | Rechecks corrected behavior and asks the independent reviewer to assess the affected correction |

Token efficiency should be evaluated on representative completed tasks, counting lead,
worker, review, and retry usage together. Compare correctness and accepted outcomes before
interpreting lower token counts as an improvement. No benchmark result is included here.
