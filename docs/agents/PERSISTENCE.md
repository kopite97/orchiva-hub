# Persistence Guidelines

## Scope

This document defines persistence rules for Orchiva Hub.

Use Spring Data JPA, PostgreSQL, and Flyway.

Follow `ARCHITECTURE.md` for package boundaries and `CONVENTIONS.md` for Java coding conventions.

## Entities

- Entities represent persistence state and must not be exposed through REST APIs.
- Prefer Lombok `@Getter` over general-purpose setters.
- Use `@NoArgsConstructor(access = AccessLevel.PROTECTED)` for JPA constructors.
- Use constructors, builders, or meaningful domain methods for state changes.
- Do not use `@Data` or unrestricted `@Setter` on entities.
- Do not expose setters for identifiers or managed timestamps.
- Keep persistence entities focused on their owning domain.

Introduce shared base entities only when common behavior justifies them.

## Relationships

- Prefer `LAZY` loading unless eager loading is explicitly required.
- Avoid unnecessary bidirectional relationships.
- Prevent N+1 queries using appropriate fetch strategies.
- Do not serialize entity relationships directly through APIs.
- Define cascade and orphan removal behavior explicitly when needed.

## Repositories

Use Spring Data JPA repositories for persistence access.

- Keep business logic out of repositories.
- Prefer derived queries for simple conditions.
- Use JPQL or native queries when necessary.
- Create custom repository implementations only when required.
- Avoid loading unnecessary entities or collections.

Repository access must follow the dependency rules in `ARCHITECTURE.md`.

## Transactions

Define transaction boundaries in the service layer.

- Use `@Transactional` for state-changing operations.
- Prefer `@Transactional(readOnly = true)` for read operations.
- Keep transactions as short as practical.
- Avoid external API calls and other slow I/O inside transactions.
- Ensure concurrent state changes preserve data consistency.
- Use appropriate locking or conditional updates when necessary.

Do not introduce complex locking strategies without a demonstrated requirement.

## Flyway Migrations

Flyway is the authoritative mechanism for database schema changes.

Store migrations under:

`src/main/resources/db/migration/`

Use sequential versioned migration names:

```text
V1__create_jobs.sql
V2__add_job_execution.sql
```

Rules:

- Inspect existing migrations before creating a new version.
- Use concise `snake_case` descriptions.
- Include only changes required by the current task.
- Never modify, rename, or delete applied migrations.
- Fix existing schema problems through new migrations.
- Preserve existing data during schema changes.
- Commit migrations with their corresponding application changes.

Do not use Hibernate automatic schema creation or updates.

Configure Hibernate to validate the schema managed by Flyway.

## Data Integrity

- Use database constraints for important invariants.
- Define unique constraints and foreign keys where appropriate.
- Add indexes based on actual query requirements.
- Use `Instant` and PostgreSQL `TIMESTAMPTZ` for absolute timestamps.
- Never store plaintext credentials or sensitive tokens.
- Avoid destructive schema changes without explicit approval.

## Verification

- Verify entity mappings against Flyway migrations.
- Test persistence queries and transaction behavior when applicable.
- Verify migrations against the configured test database.
- Never delete database volumes or bypass migrations to resolve failures.

Follow `TESTING.md` for detailed test execution rules.