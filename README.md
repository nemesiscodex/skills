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

### [Structured PR Reviewer](skills/structured-pr-reviewer/)

Provides a certainty-scored pull request review workflow with diff gathering,
context reconstruction, finding format, testing coverage checks, and final
ratings.

Give it a PR URL or a base branch. For a PR URL, `scripts/gather-pr` collects
metadata, files, commits, existing reviews, CI checks, and a worktree at the PR
head in one call. Findings are saved as drafts, and `scripts/post-review`
validates every line anchor before posting, only after you confirm. The scripts
need Python 3, `git`, and an authenticated `gh` CLI.

## Repository Layout

```text
skills/
  structured-pr-reviewer/
    GATHER.md
    SKILL.md
    scripts/
      gather-pr
      post-review
```

Each skill is self-contained in its directory. Add supporting files next to
`SKILL.md` and link to them with relative paths.

## License

MIT License

Copyright (c) 2026 Julio Daniel Reyes
