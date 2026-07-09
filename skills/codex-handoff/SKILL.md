---
name: codex-handoff
description: Hand the current Codex conversation off to a fresh Codex thread that can continue the work from a concise, redacted summary. Use when the user asks to continue work in another Codex thread, create a background handoff, fork the current task, or prepare a new session to pick up current context.
---

# Codex Handoff

Hand the current conversation to a fresh Codex continuation without copying sensitive or redundant material. Preserve enough context for the next thread to act immediately.

## Workflow

1. Determine the continuation target from the user request.
   - Default to a user-visible same-directory fork with `codex_app.fork_thread`.
   - Use a worktree fork only when the user asks for an isolated worktree or branch-style continuation.
   - Use `codex_app.create_thread` only when the user explicitly asks for a separate new thread rather than a fork of the current conversation.
   - Avoid `multi_agent_v1.spawn_agent` unless the user explicitly asks for private sub-agents or delegated internal work.
2. Write a concise handoff prompt using the contract below.
3. Redact secrets, credentials, API keys, tokens, passwords, and personal data before sending anything to another thread.
4. Send the prompt to the new or forked thread with `codex_app.send_message_to_thread` when a thread id is available.
5. Report the destination thread id and what was sent at a high level. Do not paste sensitive details back to the user.

If the needed Codex thread tools are not currently available, search for them with `tool_search` before falling back to a plain handoff summary.

## Handoff Prompt Contract

Include these sections, omitting sections that are genuinely empty:

- Current goal and user intent.
- Current repo, project, branch, workspace, and relevant environment context.
- Decisions already made.
- Work completed and current verification status.
- Remaining work and the next concrete action.
- Relevant files, plans, PRs, issues, diffs, commands, or docs by path or URL.
- Suggested skills the next thread should invoke.
- Known risks, constraints, or assumptions.

Reference existing artifacts by path or URL instead of duplicating large content already captured in PRDs, plans, ADRs, issues, commits, diffs, or docs.

## Prompt Shape

Use this shape for the message sent to the continuation thread:

```markdown
You are continuing work from a Codex handoff.

## Current Goal
...

## Context
...

## Decisions Made
...

## Work Completed
...

## Verification Status
...

## Remaining Work
...

## Relevant Artifacts
...

## Suggested Skills
...

## Risks And Assumptions
...

Start by reading the referenced artifacts and then continue with the next concrete action.
```

Tailor the title and emphasis when the user passes a focus such as "handoff for tests" or "continue the refactor".
