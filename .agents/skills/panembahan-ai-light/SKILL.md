---
name: panembahan-ai-light
description: "Use PanembahanAi-Light for daily coding, small features, and localized fixes using direct execution and focused verification; use Exact when the user requires a strict problem-only edit boundary."
---

# PanembahanAi-Light

Solve the requested daily coding task in the responsible code. Include directly necessary
supporting changes; leave unrelated cleanup and improvements out of the patch.

## Model roles

- Brain: `gpt-6-astra`, reasoning `medium`; normally performs small tasks directly.
- Focused worker when beneficial: `gpt-5.6-luna`, reasoning `max`, agent `panembahan-luna`.
- High-level worker for a hard bounded question: `gpt-6-astra`, reasoning `low`, agent `panembahan-astra-worker`.
- High-risk reviewer: fresh `gpt-6-astra`, reasoning `medium`, agent `panembahan-reviewer`.

Use configured agents or explicit model/effort arguments. A skill cannot switch the running
brain. Disclose an unavailable or mismatched model; do not silently substitute it.

## Execute

1. Identify the requested behavior and observable success condition. Inspect the responsible
   path, relevant callers or tests, and repository instructions. Preserve existing user edits.
2. Apply the smallest complete fix or feature using existing conventions. Skip a formal plan
   for straightforward work. Avoid broad scans unless the cause cannot be established locally.
3. Execute directly by default. This skill permits a bounded worker only when it avoids
   meaningful duplicated effort or answers a hard technical question. Luna gets clear tasks;
   Astra low gets judgment-heavy investigation or integration. The brain keeps scope decisions.
   Parallel tasks must be independent with non-overlapping ownership; sequence dependent edits.
4. Give any worker the mode, outcome, allowed scope, interfaces, success criteria, checks,
   and necessary context. Prohibit nested delegation and request a concise evidence report.
5. Correct one obvious mechanical mistake and recheck. For repeated or conceptual failure,
   the brain revisits evidence and changes the hypothesis before continuing.
6. Verify the changed behavior through a focused reproduction or relevant existing tests.
   Add a regression test when it guards an actual behavior gap. Run mandatory repository
   checks. Avoid broad discretionary suites, duplicate checks, and unrelated test refactors.
7. Local reversible behavior is normally normal risk. Security/authorization, money,
   destructive data changes, migrations, concurrency correctness, public compatibility,
   and production-critical impact require focused high-risk verification plus a fresh Astra
   medium reviewer. Keep both the fix and review bounded to the requested behavior.
8. Report what changed and the actual verification result. State remaining limitations;
   do not call missing required checks or review fully verified.

Continue work already authorized. Ask if a new decision or wider scope is needed for a
correct result. Do not turn daily work into a framework, incidental refactor, persisted ledger,
model escalation ladder, or state machine. Honor the latest explicitly selected mode.
