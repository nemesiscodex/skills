---
name: cursor-model-mapping
description: Cursor delegation model floors, modes, and acceptance gates.
disable-model-invocation: true
---

# Cursor Model Mapping

Map generic delegation floors to Cursor like this.

| Floor | Cursor mapping | Mode | Gate |
|---|---|---|---|
| **Scout** | Grok 4.5 Low or Auto | workspace write (scratch/findings only; do not patch application code) | Return scratch path, 3-line summary, confidence. Parent sanity-checks only. |
| **Builder** | Grok 4.5 Low (non-fast) for small patches; Grok 4.5 Medium (non-fast) when tests or logic are non-trivial | workspace write | Relevant tests/build/checks pass or the delegatee reports the blocker. |
| **Senior** | Grok 4.5 High (non-fast) | workspace write | Parent may inspect scratch notes and final diff before accepting. |
| **You** | Parent agent, preferably Grok 4.5 High or GPT-5.6 Sol | Current host permissions | No delegation. |

Prefer the lowest floor that satisfies the slice. Go up one floor when stakes, reversibility, or ambiguity are unclear.

When launching Cursor Task/subagents, pass the chosen model on the delegatee. Do not use Grok 4.5 Fast for Builder — Medium (non-fast) only.

For naming be sure to prefix the agent name with the type of agent, like 'Scout:<subagentName>'.
