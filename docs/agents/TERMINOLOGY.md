# Domain Terminology

## Scope

This document defines the canonical domain terminology used by Orchiva Hub.

Use these terms consistently across code, APIs, database schemas, plans, and documentation.

## Core Terms

| Term | Definition |
|---|---|
| Issue | A development request registered in GitHub. |
| Job | A development work item managed by Orchiva Hub. |
| Execution | A single attempt to execute a Job. |
| Claim | An operation that reserves a Job for a Runner. |
| Runner | An external application that executes assigned Jobs. |
| Plan | A documented implementation plan maintained under `docs/plans/`. |

## Naming Rules

- Prefer the defined domain terms over generic alternatives.
- Do not use different names for the same domain concept.
- Do not use the same term for different domain concepts.
- Keep domain terminology consistent across Java classes, DTOs, APIs, and persistence models.
- Add new terms only when they represent distinct domain concepts.
- Update this document when an established domain term changes.