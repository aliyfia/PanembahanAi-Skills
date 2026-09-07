---
name: panembahan-ai-exact
description: "Use PanembahanAi-Exact when the user requests only a specified problem be fixed, with strictly necessary edits and minimal decisive testing."
---

# PanembahanAi-Exact

Fix only the specified problem. Every edit must be necessary for its correct resolution.
Do not fix adjacent issues, clean up formatting, rename symbols, upgrade dependencies,
reorganize tests, or improve neighboring code unless required by that exact fix.

## Model roles

- Brain: `gpt-6-astra`, reasoning `medium`; executes directly by default.
- Optional focused worker: `gpt-5.6-luna`, reasoning `max`, agent `panembahan-luna`.
- Optional high-level worker: `gpt-6-astra`, reasoning `low`, agent `panembahan-astra-worker`.
- High-risk reviewer: fresh `gpt-6-astra`, reasoning `medium`, agent `panembahan-reviewer`.

Use configured agents or explicit model/effort settings. A skill cannot switch the running
brain. Disclose mismatches or unavailable models; do not silently substitute them.

## Execute

1. Identify the exact failure, expected behavior, and any user-specified file or edit limits.
   Define a decisive observable success condition. Read repository instructions and the
   relevant source; read-only inspection may follow dependencies without authorizing edits.
2. Establish the cause and make the smallest complete correction. Preserve user changes.
   Multiple files are allowed only if necessary and within the user's boundary. If correct
   repair requires an edit outside an explicit boundary, explain why and ask before editing it.
   Do not hide an incomplete fix behind a smaller diff.
3. Execute directly unless one bounded task materially benefits from a worker. This skill
   permits Luna for a well-defined correction and Astra low for a hard technical question.
   Pass the exact problem, edit boundary, mode, success criteria, interfaces, and checks.
   Workers must not delegate or fix anything else. Parallel work is exceptional and requires
   independent outcomes and non-overlapping ownership; sequence dependencies.
4. Permit one correction of an obvious mechanical mistake. Repeated or conceptual failure
   returns to the brain to inspect evidence and change the hypothesis. Do not silently widen
   scope or change modes because the problem is harder than expected.
5. Run the smallest decisive reproduction or relevant existing test, plus mandatory repository
   checks. Add a narrow regression test only if required or if existing checks cannot establish
   the fix and regression protection is warranted. Do not introduce a test framework or run
   broad discretionary suites. Stop retesting once criteria are met unless relevant edits,
   failures, or unresolved evidence justify another check.
6. Assess actual risk even for a one-line patch. Security/authorization, money, destructive
   data operations, migrations, concurrency correctness, public compatibility, and production-
   critical effects require focused safety evidence and a fresh Astra medium reviewer.
   Normal localized reversible changes need no independent review. Keep risk review inside
   the exact problem. If essential verification cannot be performed under the user's limits,
   report the conflict and request direction; do not claim verified completion.
7. Inspect the final diff for incidental edits. Report only the fix, actual check result, and
   any remaining limitation. Mention an adjacent issue only if it materially blocks or changes
   the safety of this fix; do not implement it without authorization.

Honor current authorization and the latest explicit mode. No planning documents, extra
features, retry frameworks, persisted ledgers, or orchestration state machines are needed.
