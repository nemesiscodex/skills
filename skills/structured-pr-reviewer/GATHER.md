# Gather PR changes

Use when git MCP is unavailable. Replace `<base-branch>` with the branch name the user provides.

## Git commands

Use three dots (`...`) for `diff` — compares against the merge base, not the tip of the base branch.
Use two dots (`..`) for `log` — lists commits on the current branch not in the base branch.

```bash
# Current branch (if needed)
git rev-parse --abbrev-ref HEAD | cat

# Default branch from remote (skip if user provided base branch)
git remote show origin | grep 'HEAD' | cat

# Changed files
git diff --name-only origin/<base-branch>...HEAD | cat

# Full diff — required, not name-only
git diff origin/<base-branch>...HEAD | cat

# Per-file diff (do not omit the -- separator)
git diff origin/<base-branch>...HEAD -- <filepath> | cat

# Commit history
git log --oneline --graph --decorate origin/<base-branch>..HEAD | cat
```

## GitHub CLI

When reviewing an open PR and `gh` is available:

```bash
# PR metadata (title/body/base/head/labels/reviews/etc.)
gh pr view --json number,title,url,state,baseRefName,headRefName,author,labels,createdAt,updatedAt,body,comments,reviews

# Human + bot PR comments (timeline-style)
gh pr view --comments
```

`gh` requires network access. In a sandbox, request network permissions.
On TLS/cert errors (e.g. `x509: OSStatus -26276`), rerun with broader permissions (outside the sandbox).
