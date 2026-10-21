# Plan Management Guidelines

## Scope

This document defines planning, approval, and progress management rules for Orchiva Hub.

Follow `../agents/WORKFLOW.md` for the overall development workflow.

Plans define implementation scope, execution steps, and verification criteria.

## Plan Files

- `README.md` → Plan index and current progress.
- `PLAN_RUNTIME_TEMPLATE.md` → Plans requiring runtime verification.
- `PLAN_NON_RUNTIME_TEMPLATE.md` → Plans requiring only static verification.
- `PLAN-XXXX-<description>.md` → Individual implementation plans.

Do not modify template files when creating individual plans.

## Plan Creation

When a plan is required:

1. Read `README.md` and review existing plans.
2. Check for overlapping or duplicate work.
3. Select the appropriate template.
4. Create a plan with a unique sequential number.
5. Set its initial status to `Planned`.
6. Register the plan in `README.md`.
7. Present the plan for approval before implementation.

Follow the authorization rules in `../agents/WORKFLOW.md`.

## Template Selection

Use `PLAN_RUNTIME_TEMPLATE.md` when verification requires application execution, APIs, databases, containers, or integration tests.

Use `PLAN_NON_RUNTIME_TEMPLATE.md` when static verification is sufficient.

Never skip required runtime verification by selecting the non-runtime template.

## Plan Status

Use the following statuses:

- `Planned` → Created but not yet activated.
- `Active` → Approved and currently being implemented.
- `On Hold` → Intentionally paused while awaiting other work or prerequisites.
- `Blocked` → Cannot proceed due to an unresolved problem.
- `Completed` → Implementation and required verification finished.
- `Cancelled` → Plan intentionally abandoned.

## Single Active Plan Rule

**Only ONE plan may have `Active` status within this project at any time.**

- Before activating a plan, check `README.md` and existing plan files.
- Never activate a plan while another plan is `Active`.
- Complete, pause, block, or cancel the current Active plan before activating another.
- Never change a plan's status solely to bypass this restriction.
- Follow `WORKFLOW.md` authorization rules when activating or resuming a plan.

This rule applies to both manual and Orchiva-managed development.

## Paused and Blocked Plans

- Use `On Hold` for intentional pauses caused by dependencies or priorities.
- Use `Blocked` when an unresolved problem prevents progress.
- Record the reason, remaining work, and resumption conditions in the plan.
- Update `README.md` immediately when the status changes.
- Resume only when the required conditions are satisfied.
- Never resume automatically without the required authorization.

## Progress Management

- Update the active plan as implementation progresses.
- Record meaningful progress, verification results, and blockers.
- Keep plan status consistent with `README.md`.
- Do not mark a plan `Completed` until required verification succeeds.
- Request approval when changes exceed the authorized scope.

## README Management

`README.md` is the central index of all plans.

It must contain only a Markdown table with these columns:

| Order | Status | Plan | Description |
|---|---|---|---|

- Register every created plan.
- Use sequential numbers for `Order`.
- Link each plan file in the `Plan` column.
- Keep descriptions short and meaningful.
- Update the corresponding row whenever a plan status changes.
- Do not add summaries, instructions, or additional sections.

## General Rules

- Keep plans focused on a single coherent objective.
- Avoid unrelated changes and speculative work.
- Preserve completed, cancelled, and paused plans as development history.
- Do not modify unrelated plans.
- Follow the selected template and applicable agent instructions.