# Configuration Guidelines

## Scope

This document defines application configuration and environment variable management for Orchiva Hub.

Deployment procedures belong to `DEPLOYMENT.md`.
Security requirements belong to `SECURITY.md`.

## Spring Configuration

- Use `application.yml` for common application settings.
- Use `application-local.yml` and `application-prod.yml` for environment-specific settings.
- Do not introduce `application.properties`.
- Select the environment using `SPRING_PROFILES_ACTIVE`.
- Reference environment-dependent values through environment variables.
- Never hard-code credentials, secrets, or environment-specific endpoints.
- Keep configuration properties grouped by responsibility.

Example:

```yaml
spring:
  datasource:
    url: ${DB_URL}
    username: ${DB_USERNAME}
    password: ${DB_PASSWORD}
```

Use default values only when they are safe and environment-independent.

Required configuration must fail clearly when missing or invalid.

## Environment Variables

Use `UPPER_SNAKE_CASE` with descriptive names.

When adding or changing an environment variable:

1. Define its usage in the appropriate Spring configuration.
2. Update `.env.example`.
3. Configure its value in the target runtime environment.
4. Verify that the application starts with the configured value.

Do not introduce environment variables for values that do not require external configuration.

## Local Environment

- Use `.env` for local development values.
- Never commit `.env` or real credentials.
- Keep `.env.example` under version control with safe placeholders.
- Never use production credentials in the local environment.

Spring Boot does not load `.env` automatically.

Inject variables through the IDE, terminal, or Docker Compose.

## Deployment Environment

- Supply production configuration and secrets outside the repository.
- Never embed secrets in Docker images, source code, or build artifacts.
- Keep environment-specific settings separate from application logic.
- Ensure required variables are passed into the application container.
- Do not assume Docker Compose `--env-file` automatically injects all variables into containers.

See `DEPLOYMENT.md` for Docker Compose and deployment configuration.

## Configuration Changes

- Update `.env.example` when variables are added, renamed, or removed.
- Remove obsolete configuration rather than retaining unused settings.
- Verify configuration binding and application startup after changes.
- Never log or expose secret values during verification.

Keep feature-specific configuration rules out of this document. If additional detailed instructions are needed, ask the user before creating a separate instruction file.