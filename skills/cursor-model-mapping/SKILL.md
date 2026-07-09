---
name: cursor-model-mapping
description: Map generic delegation capability floors to Cursor models, reasoning effort, and acceptance gates. Use with delegator or delegator-cursor when delegation should run through Cursor subagents.
disable-model-invocation: true
---

# Cursor Model Mapping

Map generic delegation floors to Cursor like this.

| Floor | Cursor mapping | Mode | Gate |
|---|---|---|---|
| **Scout** | Composer 2.5 (prefer) or Auto | read-only exploration | Return scratch path, 3-line summary, confidence. Parent sanity-checks only. |
| **Builder** | GPT-5.5 Low for small patches; Grok 4.5 Medium (non-fast) when tests or logic are non-trivial | workspace write | Relevant tests/build/checks pass or the delegatee reports the blocker. |
| **Senior** | GPT-5.5 Medium | workspace write | Parent may inspect scratch notes and final diff before accepting. |
| **You** | Parent agent, preferably Grok 4.5 High | Current host permissions | No delegation. |

Prefer the lowest floor that satisfies the slice. Go up one floor when stakes, reversibility, or ambiguity are unclear.

When launching Cursor Task/subagents, pass the chosen model on the delegatee. Do not use Grok 4.5 Fast for Builder — Medium (non-fast) only.

For naming be sure to prefix the agent name with the type of agent, like 'Scout:<subagentName>'.
