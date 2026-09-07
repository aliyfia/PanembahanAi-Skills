---
name: panembahan-ai-max
description: "Use PanembahanAi-Max for explicitly hard coding sessions, complex features, difficult refactors, or substantial engineering work requiring deeper investigation and review."
---

# PanembahanAi-Max

Deliver strong engineering for the requested outcome. Depth must address real complexity;
the mode does not authorize speculative infrastructure or unrelated improvements.

## Model roles

- Brain: `gpt-6-astra`, reasoning `medium`; owns scope, architecture, integration, and completion.
- Focused worker: `gpt-5.6-luna`, reasoning `max`, custom agent `panembahan-luna`.
- High-level worker: `gpt-6-astra`, reasoning `low`, custom agent `panembahan-astra-worker`.
- Independent reviewer: fresh `gpt-6-astra`, reasoning `medium`, custom agent `panembahan-reviewer`.

Use configured agents or explicit model/effort settings in the available delegation tool.
A skill cannot change the parent model; disclose a mismatch or unavailable model. Do not
silently substitute. The brain can execute directly when delegation adds no benefit.

## Execute

1. Establish observable acceptance criteria, constraints, and affected interfaces. Read
   repository instructions and trace the relevant architecture. Keep existing user edits.
2. Identify consequential tradeoffs and failure modes. Use a short plan sized to the work;
   write design documentation only when it helps implement or maintain the requested change.
3. Classify risk from impact. Security/authorization, money, destructive data changes,
   migrations, concurrency correctness, public compatibility, and production-critical behavior
   require high-risk treatment. Other localized reversible changes are normally normal risk.
4. Implement cohesive changes. This skill authorizes bounded subagents when useful:
   Luna for well-defined work; Astra low for difficult integration or investigation requiring
   judgment. Delegate parallel tasks only with independent outcomes and non-overlapping write
   ownership. Sequence dependent changes. Keep architectural decisions with the brain.
5. Supply each worker the mode, outcome, edit boundary, interfaces, acceptance criteria,
   relevant context, and checks. Prohibit nested delegation. Request concise evidence back.
6. For an obvious mechanical failure, allow one correction and recheck. Repeated or conceptual
   failure returns to the brain: inspect evidence, revise the hypothesis, then choose a new
   approach. Do not pass the same failing plan repeatedly between models.
7. Verify acceptance criteria, relevant regressions and integration, and meaningful failure
   paths. Check compatibility, rollback, security, or performance only where impact warrants it.
   Run repository-required checks. Broaden tests for demonstrated gaps, not ceremony.
8. Use a fresh independent reviewer for substantial changes and every high-risk change.
   Give it the request, current diff, source access, identified risks, and actual evidence.
   Resolve material findings and recheck affected paths after corrections.
9. Report the outcome, actual checks and their results, and remaining limitations. Required
   verification or review gaps prevent a fully verified completion claim.

Continue authorized work without repeated approval requests. Ask only for missing decisions
that materially affect the outcome or new authority. If a selected strict boundary prevents
a correct fix, explain it before expanding. Do not add event ledgers, retry frameworks, model
ladders, or orchestration state machines. The latest explicitly selected mode governs.
