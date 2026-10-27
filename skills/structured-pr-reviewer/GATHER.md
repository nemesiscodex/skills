# Gather a local branch

For a PR URL, use `scripts/gather-pr` instead. Replace `<base-branch>` with the branch name the user provides.

Use three dots (`...`) for `diff` — compares against the merge base, not the tip of the base branch.
Use two dots (`..`) for `log` — lists commits on the current branch not in the base branch.

```bash
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

`gh` and `git fetch` need network access. On TLS/cert errors in a sandbox (e.g. `x509: OSStatus -26276`), rerun outside the sandbox.
