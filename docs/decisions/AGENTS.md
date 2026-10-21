# Decision Management Guidelines

## Scope

This document defines how architectural and technical decisions are recorded and maintained.

Decisions preserve important design choices and their rationale for future development.

Unlike Plans, Decisions do not track implementation progress.

## Decision Files

- `README.md` → Index of recorded decisions.
- `DECISION-XXXX-<description>.md` → Individual decision records.

Use sequential numbers and concise, descriptive filenames.

No separate Decision template is required.

## Decision Creation

1. Review existing decisions to avoid duplicates or conflicts.
2. Create a new Decision when an important technical or architectural choice is approved.
3. Assign the next available sequential number.
4. Describe the objective and the chosen approach.
5. Register the Decision in `README.md`.

Do not make significant architectural decisions without the required user approval.

## Decision Content

Each Decision must contain:

- **Objective** → What problem or design question the decision addresses.
- **Description** → The chosen approach and the reasoning behind it.

Keep records concise and focused on a single decision.

Do not include implementation steps, progress tracking, or detailed execution rules.

## Decision Maintenance

- Treat accepted decisions as historical records.
- Do not silently overwrite or remove existing decisions.
- When replacing a decision, create a new record and reference the previous one.
- Preserve the reasoning behind superseded decisions.
- Follow applicable decisions during implementation.

## README Management

`README.md` is the central index of all decisions.

- Register every created Decision.
- Use sequential numbers in the `Order` column.
- Link each Decision file.
- Keep descriptions short and meaningful.
- Do not add unrelated sections or instructions.