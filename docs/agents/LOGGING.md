# Logging Guidelines

## Scope

This document defines application logging and diagnostic rules for Orchiva Hub.

Use logs to trace significant operations and diagnose failures.

Job states and execution records must be persisted separately. Logs are not the source of truth.

## Logging Framework

- Use SLF4J with Spring Boot's default Logback implementation.
- Prefer Lombok `@Slf4j` for logger declarations.
- Use parameterized logging with `{}` placeholders.
- Write logs to console output.
- Do not introduce custom logging frameworks or infrastructure without a requirement.

## Log Levels

- `ERROR` → Unexpected failures or operations that cannot complete.
- `WARN` → Recoverable failures or abnormal conditions requiring attention.
- `INFO` → Significant business events and state changes.
- `DEBUG` → Detailed diagnostics, polling activity, and retry information.

Do not log routine successful polling or expected empty results at `INFO`.

Expected validation failures and claim conflicts must not be treated as server errors.

## Important Events

Log meaningful events when applicable:

- GitHub Issue synchronization and Job registration.
- Successful Job claims and execution state changes.
- Execution completion or failure.
- External API failures and significant retry exhaustion.
- Application startup and critical configuration failures.

Avoid logging the same event at multiple layers.

## Logging Context

Include relevant identifiers when available:

- `jobId`
- `executionId`
- `runnerId`
- `issueNumber` and repository identifier
- `requestId` for HTTP request correlation

Use consistent field names across application logs.

Generate request identifiers on the server and associate them with request logs through MDC when applicable.

Clear MDC context after request processing to prevent information leakage between requests.

## Error Logging

- Log exceptions at the layer responsible for handling the failure.
- Include stack traces for unexpected failures when needed.
- Avoid logging and rethrowing the same exception repeatedly.
- Use concise messages that identify the failed operation and relevant context.
- Never suppress errors without appropriate handling or reporting.

## Sensitive Information

Never log:

- Passwords, access tokens, API keys, or credentials.
- Authorization headers or session identifiers.
- Complete request or response bodies containing sensitive data.
- Environment variable values containing secrets.
- Raw Codex prompts or potentially sensitive execution output.

Log only the information necessary for diagnostics.

## Environment Rules

- Use `application.yml` and environment profiles to configure logging levels.
- Keep production logging at `INFO` by default.
- Enable `DEBUG` selectively when troubleshooting.
- Avoid verbose SQL logging in production.
- Follow `CONFIGURATION.md` for environment-specific settings.

## Verification

- Verify important operations produce meaningful logs.
- Ensure polling does not generate excessive output.
- Confirm exceptions are recorded without duplicate stack traces.
- Verify that sensitive information is never exposed.

Detailed log aggregation, retention, and monitoring infrastructure are outside this document. Propose separate instructions when required.