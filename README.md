# PanembahanAi

Four coding modes with one model hierarchy. Choose how much engineering the task needs; keep acceptance criteria and honest completion evidence in every mode.

| Role | Model | Reasoning | Responsibility |
| --- | --- | --- | --- |
| Brain | `gpt-6-astra` | `medium` | Understand the problem, choose the approach, assign work when useful, integrate and verify |
| Worker | `gpt-5.6-luna` | `max` | Implement well-defined tasks with clear boundaries |
| High-level worker | `gpt-6-astra` | `low` | Investigate or implement work requiring judgment across components |
| Independent reviewer, when needed | `gpt-6-astra` | `medium` | Fresh read-only review; does not review its own implementation |

These assignments stay the same in all modes. **Max is the mode name, not the brain's reasoning level.**

## Choose a mode

| Mode | Use it for | Scope and coordination | Verification |
| --- | --- | --- | --- |
| **PanembahanAi-Max** | Hard coding sessions, complex features, difficult refactors | Trace affected architecture; compare material tradeoffs; delegate independent work when useful | Relevant unit/integration checks, meaningful failure paths, independent review of substantial changes |
| **PanembahanAi-Mid** | Medium features and changes spanning a few components | Short plan; use existing patterns; delegate only when it reduces total work | Acceptance criteria, relevant regression and integration checks; independent review for high risk |
| **PanembahanAi-Light** | Daily fixes and small features | Direct execution by default; edit the responsible code and directly necessary supporting code | Focused reproduction or existing checks; add a regression test when it adds useful protection |
| **PanembahanAi-Exact** | One precise reported problem | Strict problem boundary; smallest complete correction; no incidental cleanup or sibling fixes | Smallest decisive check plus mandatory repository checks; no broad discretionary test sweep |

Light can include a small supporting change needed to make the requested behavior work. Exact requires every edit to be necessary for the specified problem. Neither mode authorizes unrelated improvements. A complete fix may require more than one file.

Mid aims to save tokens through narrow context, short handoffs, fewer agents, and avoiding repeated checks. Savings and equal outcomes are design goals, not measured guarantees. Uncertainty that affects correctness deserves investigation in every mode.

## Use in Codex

This repository contains instructions and native Codex configuration, not a standalone orchestration service.

1. Copy the four folders in `.agents/skills/` into your target project's `.agents/skills/` directory.
2. Merge `.codex/config.toml` into that project's configuration and copy `.codex/agents/` into its matching directory. Preserve existing settings and conflicting files deliberately.
3. Start a new task with **Astra / medium** selected. A skill cannot change the model already running the parent task.
4. Invoke one mode explicitly:

```text
$panembahan-ai-max Implement this migration with compatibility and rollback coverage.
$panembahan-ai-mid Add pagination to this endpoint using the existing API conventions.
$panembahan-ai-light Fix the settings form losing its saved value.
$panembahan-ai-exact Fix this null crash. Change only what is necessary for this crash.
```

Natural-language names such as “PanembahanAi Light” mean the same thing. Select one mode at a time; if a later request selects a different mode, use it for the remaining work. Use Light for an unspecified daily coding task, Mid for a clearly medium feature, and Max for explicitly hard engineering work. Do not silently widen an explicit Exact request.

The model identifiers and reasoning levels must be available on your host. If a requested model is unavailable, disclose it and ask for a substitute when delegation is required. Direct execution is still appropriate when the lead can complete the task. Never claim a model was used merely because a prompt requested it.

## Shared operating rules

- Define observable acceptance criteria before editing. Example: “Missing optional input returns the documented response; valid input still works; the relevant check passes.”
- Inspect the responsible path and repository instructions. Respect the user's existing changes and authorized scope.
- Delegate only a concrete bounded task when the benefit exceeds the handoff cost. Parallel writers need independent outcomes and non-overlapping ownership; sequence dependent edits.
- Give workers the outcome, allowed files or component, interfaces, mode, checks, and relevant evidence. Workers return changes, actual check results, and unresolved issues. They do not create their own worker hierarchy.
- A clear mechanical mistake gets one correction and recheck. A repeated failure or a conceptual problem returns to the Astra medium brain for a new hypothesis. Do not cycle models through the same failed plan.
- Normal risk means localized, reversible behavior with bounded impact. High risk includes security or authorization boundaries, money movement, destructive data changes, migrations, concurrency correctness, public compatibility, and production-critical paths. Assess actual impact, not file size.
- For high risk, use focused safety checks and a fresh Astra medium reviewer in any mode. Keep review scoped to the change. Exact limits discretionary testing; it does not waive repository requirements or justify declaring unsafe work complete.
- Finish with what changed, evidence for each acceptance criterion, and any remaining limitation. If a required check or independent review is unavailable, report that gap and do not call the work fully verified.

Scope and verification are separate: a risky one-line fix can need careful verification without becoming a larger refactor. If a correct fix requires widening an explicit edit boundary, explain the dependency and ask before doing that additional work.

There is no persisted event ledger, retry counter system, mandatory planning document, Terra routing, or state-machine service.

## Files and validation

Each skill is self-contained so it can be copied independently. Agent definitions supply the model configuration; the selected skill supplies the mode rules. `docs/behavior-checks.md` lists representative scenarios for evaluating these instructions. Syntax validation does not prove model behavior or token savings.

Configuration follows the official [Codex subagent documentation](https://learn.chatgpt.com/docs/agent-configuration/subagents). Astra supports the requested low and medium settings in the [model documentation](https://developers.openai.com/api/docs/models/gpt-6-astra). Host support must still be checked when using the files.

No license is included because no license preference was supplied.
