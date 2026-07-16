# Engineering Workflow

This repository packages a Codex-oriented Engineering Workflow skill set plus a visual HTML guide for using it.

## Start Here

For a new repository:

1. Run `setup-engineering-workflow` once.
2. Start project work with `project-shaping`.
3. Continue through `to-spec`.
4. Break work down with `to-tickets`.
5. Deliver one ticket at a time with `deliver-ticket`.
6. Repeat ticket selection only after the current ticket is finalized.

Open `engineering-workflow-guide.html` for the full clickable workflow guide.

## Included Skills

The workflow skills are stored under `skills/`:

- `setup-engineering-workflow`
- `project-shaping`
- `to-spec`
- `to-tickets`
- `deliver-ticket`
- `implement`
- `tdd`
- `code-review`
- `wayfinder`
- `triage`
- `diagnosing-bugs`
- `improve-codebase-architecture`
- `grilling`
- `domain-modeling`
- `research`
- `prototype`
- `codebase-design`
- `codex-handoff`

## Recommended Flow

The main delivery path is:

```text
setup-engineering-workflow, once per repo
  -> project-shaping
  -> to-spec
  -> to-tickets
  -> deliver-ticket
       -> implement + tdd + code-review + PR/finalize
       -> repeat for the next eligible ticket
```

Use the support skills when the work calls for them:

- `wayfinder` for large, foggy work that needs investigation tickets.
- `triage` for incoming issues and external PRs.
- `diagnosing-bugs` for failures, regressions, slowness, and flaky behavior.
- `improve-codebase-architecture` for codebase health work.
- `domain-modeling`, `research`, `prototype`, and `codebase-design` to reduce planning and design risk.
- `codex-handoff` to move current context into a fresh Codex thread.
