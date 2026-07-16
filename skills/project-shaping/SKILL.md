---
name: project-shaping
description: Shape a product idea, project plan, or design into a clear, documented plan with domain language, decisions, risks, and technical foundation. Use when starting a new project, preparing a major feature, pressure-testing a design before specs, or deciding whether research, prototype, or codebase-design is needed before to-spec.
---

# Project Shaping

Shape the work before it becomes a spec. This skill orchestrates `grilling` and `domain-modeling`: ask hard questions, resolve the important decisions, and record durable terminology or ADR-worthy choices as they crystallize.

## Core Loop

1. Classify the work as one of:
   - **New project** - a repo/product is being started or the technical foundation is not chosen.
   - **Existing feature** - the repo and stack already exist; the work should fit the current system.
   - **Architecture change** - the main uncertainty is module shape, interfaces, seams, or codebase structure.
   - **Unclear** - ask one classification question before continuing.
2. Explore first when facts are discoverable from the repo or existing docs. Ask the user only for decisions and preferences.
3. Ask one question at a time. For every question, provide a recommended answer and the tradeoff it implies.
4. Use `domain-modeling` while shaping: name domain concepts, sharpen relationships, update glossary entries, and offer ADRs for durable decisions.
5. Do not write a spec or implementation. Stop when the plan is ready for `to-spec`, or route to the support skill needed to reduce risk.

## New Project Technical Foundation

For a new project, cover both product intent and practical technical foundation before handoff:

- Product: target users, core workflows, success criteria, non-goals, and first release boundary.
- Surfaces: web, mobile, desktop, API, admin console, CLI, background worker, or integration-only.
- Stack: language, framework, runtime, package manager, and any hard constraints from the user or hosting environment.
- Application shape: frontend/backend split, API style, state ownership, and where business rules live.
- Data: database, schema ownership, migrations, storage, retention, imports/exports, and reporting needs.
- Identity and permissions: auth provider, roles, tenancy, session model, and account lifecycle.
- Integrations: third-party APIs, webhooks, email, payments, notifications, AI services, queues, and scheduled jobs.
- Operations: deployment target, environments, local dev, secrets, CI, tests, logging, monitoring, backups, and rollback expectations.
- Quality constraints: security, privacy, compliance, accessibility, performance, scale, reliability, budget, and maintenance limits.

Keep this practical: ask only the next decision needed to make the plan safe. Do not run a full architecture audit unless the user asks for it.

Record durable technical choices as ADR candidates, especially stack, persistence, auth, deployment, integration, and major boundary decisions.

## Existing Feature Or Existing Repo

For existing work, default to the repo's current stack and architecture. Explore the codebase and docs before asking technical questions. Only challenge the stack when:

- the user proposes a stack or architecture change,
- the requested feature conflicts with current architecture,
- the current system lacks a safe test or integration seam,
- or the change introduces new data, auth, deployment, security, or operational responsibilities.

## Routing

- Use `research` when a decision depends on current external facts, service capabilities, pricing, legal constraints, or library behavior.
- Use `prototype` when a risky UI, state model, algorithm, integration, or developer-experience question can be answered cheaply.
- Use `codebase-design` when module boundaries, interfaces, seams, adapters, or testability need design before the spec.
- Hand off to `to-spec` only when product intent, domain language, important technical decisions, risks, and out-of-scope boundaries are clear.
