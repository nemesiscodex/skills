---
name: codex-model-mapping
description: Map generic delegation capability floors to Codex CLI models, reasoning effort, sandboxes, and acceptance gates. Use with delegator or delegator-codex when delegation should run through Codex.
---

# Codex Model Mapping

Map generic delegation floors to Codex like this.

| Floor | Codex mapping | Sandbox | Gate |
|---|---|---|---|
| **Scout** | `codex exec -m gpt-5.5` with `model_reasoning_effort="low"` | `read-only` | Return scratch path, 3-line summary, confidence. Parent sanity-checks only. |
| **Builder** | `codex exec -m gpt-5.5` with `model_reasoning_effort="low"` for small patches, `medium` when tests or logic are non-trivial | `workspace-write`; use `--full-auto` only when edits are required | Relevant tests/build/checks pass or the delegatee reports the blocker. |
| **Senior** | `codex exec -m gpt-5.5` with `model_reasoning_effort="medium"` | `workspace-write`; escalate sandbox only when the task genuinely needs network or broader access | Parent may inspect scratch notes and final diff before accepting. |
| **You** | Parent agent | Current host permissions | No delegation. |

Prefer the lowest floor that satisfies the slice. Go up one floor when stakes, reversibility, or ambiguity are unclear.
