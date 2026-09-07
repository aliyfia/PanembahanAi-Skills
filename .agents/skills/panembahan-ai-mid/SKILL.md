---
name: panembahan-ai-mid
description: "Use PanembahanAi-Mid for medium coding features or fixes across a few components, preserving correctness with brief planning and selective delegation."
---

# PanembahanAi-Mid

Complete medium engineering work with a short path from diagnosis to verified result.
Save tokens through focused context and coordination, never by omitting necessary reasoning.

## Model roles

- Brain: `gpt-6-astra`, reasoning `medium`.
- Focused worker: `gpt-5.6-luna`, reasoning `max`, custom agent `panembahan-luna`.
- High-level worker: `gpt-6-astra`, reasoning `low`, custom agent `panembahan-astra-worker`.
- High-risk reviewer: fresh `gpt-6-astra`, reasoning `medium`, custom agent `panembahan-reviewer`.

Use configured agents or explicit model/effort settings. A skill cannot switch the parent
model. Disclose unavailable or mismatched models; do not silently substitute them.

## Execute

1. State observable acceptance criteria and inspect the responsible components, interfaces,
   existing tests, and repository instructions. Preserve user edits. Make a brief working plan.
2. Use existing patterns. Add abstractions or dependencies only when necessary for this
   outcome. Read additional context when evidence shows it matters.
3. Prefer direct execution for a cohesive change. This skill authorizes bounded delegation
   when its benefit exceeds briefing and integration cost. Luna handles clear implementation;
   Astra low handles uncertain root causes or judgment across components. The brain decides
   architecture and scope and may handle hard questions itself.
4. Parallelize only independent outcomes with non-overlapping write ownership. Sequence
   dependencies. Give workers the mode, outcome, edit boundary, interfaces, acceptance
   criteria, relevant evidence, and checks. Workers must not delegate further.
5. Correct one obvious mechanical mistake and recheck. A repeated or conceptual failure
   goes to the brain for evidence review and a changed hypothesis, not repeated model handoffs.
6. Run acceptance and relevant regression checks, plus integration checks where interfaces
   change. Add tests for real behavior gaps; avoid redundant suites and prose restating diffs.
   Always honor mandatory repository checks. Repeat checks only after relevant changes or failures.
7. Treat localized reversible behavior as normal risk. For security/authorization, money,
   destructive data operations, migrations, concurrency correctness, public compatibility,
   or production-critical impact, perform focused high-risk checks and spawn a fresh Astra
   medium reviewer. Review the actual diff and resolve material findings. High risk increases
   necessary verification, not permission to expand implementation scope.
8. Finish with changes, actual check results linked to acceptance criteria, and remaining
   limitations. Disclose missing required verification or review; do not claim fully verified work.

Continue within existing authorization. Ask when an unresolved user choice or scope expansion
is required. Do not silently switch the chosen mode, promise measured token savings, or add
mandatory spec files, persisted ledgers, retry frameworks, or orchestration state machines.
