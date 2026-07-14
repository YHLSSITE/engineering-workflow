---
name: deliver-ticket
description: Run one Engineering Workflow ticket through the delivery loop. Use when the user asks to deliver, implement, finish, finalize, or choose the next ticket; asks for the full ticket loop; or wants implementation, TDD, checks, code review, PR, merge, and ticket completion handled as one controlled workflow.
---

# Deliver Ticket

Deliver exactly one ticket through a controlled loop. This skill orchestrates `implement`, `tdd`, and `code-review`; it does not replace their detailed instructions.

## Delegation

Use sub-agents when independent work can run in parallel without mutating the branch: ticket/spec cross-checks, codebase reconnaissance, test seam proposals, risk scans, or focused review of a tricky area. Keep branch creation, code edits, commits, pushes, merges, and final scope decisions in the main agent. If sub-agents are unavailable, do the work inline and report that fallback.

## Branches

### 1. No Ticket Chosen

If the user has not named a ticket, find the **frontier**: tickets whose blockers are complete.

Recommend one ticket and stop. Prefer the smallest frontier ticket that delivers visible product value or unlocks other tickets. Include the reason, blockers checked, and the prompt the user can send to approve it.

Completion criterion: exactly one ticket is recommended and no implementation starts.

### 2. Deliver A Named Ticket

Use this branch when the user names a ticket to implement or deliver.

1. Pin the ticket.
   - Read the ticket, acceptance criteria, linked spec, comments, and blocker list.
   - Confirm the ticket's blockers are complete.
   - State the ticket scope in one short paragraph.

   Completion criterion: the ticket, source material, blockers, and fixed point are known.

2. Prepare a dedicated branch.
   - Use the repo's branch convention; otherwise use `codex/ticket-<number>-<slug>`.
   - Preserve unrelated local changes.
   - Compare against `main` unless the user gives another base.

   Completion criterion: the branch and base are explicit.

3. Implement the ticket.
   - Use `implement` for the ticket work.
   - Use `tdd` at agreed public seams where practical. If seams are missing and not obvious from the ticket, ask before writing tests.
   - Delegate independent read-only investigation or test-seam analysis to sub-agents when it would reduce risk or latency.
   - Keep the slice vertical and limited to this ticket.

   Completion criterion: the ticket behavior is implemented and no next-ticket work is included.

4. Verify and commit.
   - Run relevant focused checks while working.
   - Run the repo's required final checks, plus `git diff --check` when available.
   - Commit the completed ticket work with the ticket reference.

   Completion criterion: checks are reported and the ticket work is committed.

5. Review and fix.
   - Use `code-review` against `main` or the chosen base.
   - `code-review` should run its Standards and Spec reviews in parallel sub-agents. If sub-agent review is unavailable, run the same two-axis review manually: Standards and Spec.
   - Fix blocking findings on the same branch, rerun relevant checks, and commit fixes.

   Completion criterion: review is clean or remaining findings are explicitly non-blocking.

6. Publish the PR.
   - Push the branch and open a PR when the environment and permissions allow it.
   - Include summary, checks run, code-review result, and ticket closing/reference text.
   - If PR creation is blocked, prepare the PR title/body and say exactly what remains blocked.

   Completion criterion: the PR is opened, or the PR draft is ready with the blocking reason.

Stop after publishing the PR. Report the ticket, branch, commits, checks, review result, PR link or draft status, and the next action for this same ticket.

### 3. Finalize A Ticket PR

Use this branch only when the user asks to finalize, merge, or complete an already delivered ticket.

1. Check the PR, CI, review state, and ticket status.
2. If anything is not green, diagnose it, fix it on the same branch, rerun checks, commit, and push.
3. If green, merge according to repo policy and mark the ticket complete.
4. Clean up ticket labels before or when closing the ticket:
   - Remove the AFK-ready label, normally `ready-for-agent` unless `docs/agents/triage-labels.md` maps it differently.
   - Add the completion label, normally `completed` unless `docs/agents/triage-labels.md` maps it differently.
5. Return to a clean, synced main branch when that is the repo convention.

Completion criterion: the ticket is merged and marked complete, `ready-for-agent` is gone, `completed` is present, or the blocker is named with the next concrete action.

Stop after finalizing this ticket. Return to ticket selection only when the user asks for the next ticket.
