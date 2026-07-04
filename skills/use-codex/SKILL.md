---
name: use-codex
description: Run Codex CLI as a subagent with gpt-5.5 at low or medium effort.
disable-model-invocation: true
---

# Use Codex

You have access to the Codex CLI, as a cheaper source of GPT-5.5 calls.

Treat Codex as a **subagent**: hand it a prompt, wait for the result, report back.

## Steps

1. **Pick effort and sandbox.** Effort is `low` or `medium` (default `medium`). Sandbox is `read-only` (default, review), `workspace-write` (edits), or `danger-full-access` (network/broad). Edits and network need `--full-auto`.
   Done when: effort and sandbox are chosen.

2. **Run `codex exec` synchronously** using the command shape below. Repo-exploration tasks at `medium` routinely take 3–7 minutes; set the shell's block/wait time above the expected runtime (e.g. 540s for a task that reads code and writes a doc). Background only if required; then timeout is 150s (`low`) or 600s (`medium`).
   Done when: the process exits and stdout is captured. Killing early yields empty output — never treat that as success.

3. **Report.** Summarize stdout. On non-zero exit, stop and report; do not retry without direction. Mention the session can be resumed.
   Done when: the user has the outcome (summary on success, failure report on error).

## Command shape

```bash
codex exec \
  --skip-git-repo-check \
  -m gpt-5.5 \
  --config model_reasoning_effort="<low|medium>" \
  --sandbox <read-only|workspace-write|danger-full-access> \
  [--full-auto] \
  [-C <DIR>] \
  "prompt" \
  </dev/null 2>/tmp/codex-stderr.log
```

Always: `--skip-git-repo-check`, `-m gpt-5.5`, effort `low|medium`, `</dev/null` (stdin must be closed or Codex hangs), `2><file>` (hides thinking tokens from output but keeps them diagnosable — on failure, tail the log instead of flying blind; `2>/dev/null` is acceptable only for throwaway calls).

## Running from Cursor's Shell tool

- Codex cannot start inside Cursor's command sandbox: it dies with `failed to initialize in-process app-server client: Operation not permitted` (exit 1, empty stdout). Requesting `full_network` is NOT enough. Always run the Shell tool with `required_permissions: ["all"]` on the first try.
- Codex has its own sandbox on top: with `--sandbox workspace-write`, network is still blocked inside Codex, so Gradle/npm downloads and build daemons fail (`SocketException: Operation not permitted`). Don't ask Codex to verify with networked builds or tests unless using `danger-full-access`; run the verification yourself afterward.
- After the command exits, verify the expected artifact exists (e.g. `test -s <output-file>`) rather than trusting exit code alone.

## Resume

Inherits model, effort, and sandbox — do not re-pass config unless the user asks:

```bash
echo "follow-up" | codex exec --skip-git-repo-check resume --last 2>/dev/null
```

Any flags go between `exec` and `resume`.
