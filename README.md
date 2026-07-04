# Agent Skills

Reusable agent skills for AI coding assistants, including Codex, Claude Code,
Cursor, OpenCode, and other tools compatible with the open Agent Skills format.

## Install

Install every skill from this repository:

```bash
npx skills add nemesiscodex/prompts
```

Install a single skill:

```bash
npx skills add nemesiscodex/prompts --skill use-codex --agent codex
npx skills add nemesiscodex/prompts --skill delegator --agent codex
npx skills add nemesiscodex/prompts --skill codex-model-mapping --agent codex
npx skills add nemesiscodex/prompts --skill delegator-codex --agent codex
npx skills add nemesiscodex/prompts --skill structured-pr-reviewer --agent codex
```

List the skills available before installing:

```bash
npx skills add nemesiscodex/prompts --list
```

The `skills` CLI discovers skill directories containing a `SKILL.md` file with
`name` and `description` frontmatter. This repository uses the standard
`skills/<skill-name>/SKILL.md` layout.

## Skills

### [Use Codex](skills/use-codex/)

Cursor-oriented workflow for running the Codex CLI as a synchronous subagent
with GPT-5.5 at low or medium reasoning effort. Use it when Cursor should hand
off a bounded prompt to Codex, wait for stdout, then summarize the result.

### [Delegator](skills/delegator/)

Defines a parent-only orchestration workflow for decomposing work, routing
slices by capability floor, keeping delegatee output in scratch files, and
preserving final judgment in the parent agent. Host-specific model names belong
in local adapters, not in the core skill.

This skill expects scratch output to live under `.run-result/`, which is
ignored by this repository.

### [Delegator Codex](skills/delegator-codex/)

Thin Codex-specific wrapper around the generic delegator workflow. It loads the
generic delegator skill plus a Codex model mapping for `Scout`, `Builder`,
`Senior`, and `You`.

Install it together with `delegator` and `codex-model-mapping`, or install all
skills from the repository.

### [Codex Model Mapping](skills/codex-model-mapping/)

Maps the generic delegation floors to Codex CLI model, reasoning effort,
sandbox, and acceptance gates. Use it directly with `delegator` or through
`delegator-codex`.

### [Structured PR Reviewer](skills/structured-pr-reviewer/)

Provides a certainty-scored pull request review workflow with diff gathering,
context reconstruction, finding format, testing coverage checks, and final
ratings.

Use it by asking an installed agent to review a pull request or branch diff.

## Repository Layout

```text
skills/
  codex-model-mapping/
    agents/
      openai.yaml
    SKILL.md
  delegator/
    SKILL.md
  delegator-codex/
    agents/
      openai.yaml
    SKILL.md
  structured-pr-reviewer/
    GATHER.md
    SKILL.md
  use-codex/
    SKILL.md
```

Each skill is self-contained in its directory. Add supporting files next to
`SKILL.md` and link to them with relative paths.

## License

MIT License

Copyright (c) 2026 Julio Daniel Reyes
