# Deployment Guidelines

## Scope

This document defines build, runtime, and deployment rules for Orchiva Hub.

Environment variables and application profiles are managed in `CONFIGURATION.md`.

## Environments

### Local

- Run Spring Boot locally through the IDE or Gradle Wrapper.
- Run PostgreSQL using Docker Compose.
- Run Orchiva Runner as a separate local application.
- Use the `local` Spring profile.

### Production

- Deploy Orchiva Hub and PostgreSQL to the personal Ubuntu server using Docker Compose.
- Orchiva Runner operates independently on a Windows machine.
- Use the `prod` Spring profile.
- Runner initiates communication with Hub over authenticated HTTPS.

Keep application behavior consistent across environments.

## Build and Runtime

- Use the Gradle Wrapper for builds.
- Package the application as an executable JAR.
- Use Docker for production deployment.
- Manage application containers through Docker Compose.
- Keep Hub and PostgreSQL as separate services.
- Do not include Runner execution logic in the Hub container.

## Deployment Rules

- Never commit credentials or production secrets.
- Supply environment-specific configuration at runtime.
- Do not expose PostgreSQL directly to the public network.
- Do not expose development-only endpoints in production.
- Preserve persistent database storage when replacing containers.
- Never deploy without explicit authorization.

## Verification

Before deployment:

1. Verify the application builds successfully.
2. Run applicable automated tests.
3. Verify database connectivity and migrations.
4. Confirm environment configuration is valid.

After deployment:

1. Verify application startup and health.
2. Confirm database connectivity.
3. Verify required API endpoints are accessible.
4. Check application logs for startup errors.

Follow `TESTING.md` for detailed verification rules.

## Future Deployment

CI/CD pipelines, container image management, network routing, and recovery procedures will be defined when production deployment is implemented.

Do not introduce deployment infrastructure before it is required.