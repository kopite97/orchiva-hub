# Security Guidelines

## Scope

This document defines minimum security requirements for Orchiva Hub.

Orchiva is a personal development automation system.
Do not introduce unnecessary user management or RBAC.

## API Security

- Restrict Hub API access to authorized clients.
- Bind local development services to loopback interfaces.
- Require authenticated HTTPS for remote Runner communication.
- Never trust a Runner ID supplied without authentication.
- Reject unauthorized Job claims and execution reports.

## GitHub Integration

- Use access tokens with the minimum required permissions.
- Process Issues only from explicitly allowed repositories.
- Treat GitHub Issue content as untrusted input.
- Never execute arbitrary commands directly from Issue content.

## Secrets

- Store credentials and API tokens outside source code.
- Never commit secrets to Git.
- Never expose secrets through API responses or logs.
- Follow `CONFIGURATION.md` for environment variable management.

## Operations

- Restrict Swagger and internal endpoints in production.
- Never allow automatic merging or deployment without authorization.
- Do not weaken security controls to bypass failures.