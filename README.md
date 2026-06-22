# Agent Skills

A collection of reusable agent skills for AI coding assistants, including Codex,
Claude Code, Cursor, OpenCode, and other tools compatible with the open Agent
Skills format.

## Install

Install every skill from this repository:

```bash
npx skills add nemesiscodex/prompts
```

Install only the structured PR reviewer, targeting Codex:

```bash
npx skills add nemesiscodex/prompts --skill structured-pr-reviewer --agent codex
```

List the skills available before installing:

```bash
npx skills add nemesiscodex/prompts --list
```

The `skills` CLI discovers skill directories containing a `SKILL.md` file with
`name` and `description` frontmatter. This repository uses its standard
`skills/<skill-name>/SKILL.md` layout.

## Available skills

### [Structured PR Reviewer](skills/structured-pr-reviewer/)

Conduct a thorough pull request review with certainty scores, reasoning,
focused findings, and quality ratings.

Use it by asking an installed agent to review a pull request or branch diff.

## License

MIT License

Copyright (c) 2026 Julio Daniel Reyes
