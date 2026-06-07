# pi-sub

A wrapper around `pi --mode json` for calling Pi non-interactively from other agents/scripts.

## Behavior

- Streams denoised live progress to stderr.
  - Visible assistant text is streamed.
  - Tool calls are summarized.
  - Optional `--show-tool-output` shows short tool result snippets on stderr.
- Emits a clean stdout transcript:
  - model/workdir/provider header
  - every visible assistant message
  - summarized tool calls
  - session id

This avoids losing earlier assistant messages when Pi says something useful, then uses more tools, then ends with a shorter final summary.

Use `--final-only` to restore the older stdout behavior that prints only the final assistant answer.
