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

## OpenAI Codex Fast mode

When Arthur's Pi Fast extension is installed, `pi-sub` passes `--fast` through to Pi and surfaces the extension's eligibility/result notice on stderr:

```bash
pi-sub --fast "Investigate this bug"
pi-sub --fast --thinking high "Investigate this bug deeply"
pi-sub --fast resume SESSION_ID "Continue in Fast mode"
```

Fast mode is per invocation. Omit `--fast` for Standard mode, and pass it again when resuming a session. Nested Pi subagents are separate processes and intentionally remain Standard.
