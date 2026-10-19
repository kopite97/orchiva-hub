# Orchiva Hub — Project Overview

## Purpose

Orchiva is an AI-powered development automation system that processes GitHub Issues through local AI workers.

Orchiva Hub is the Spring Boot server responsible for coordinating development automation.

The system must remain usable without optional AI assistants such as ChatGPT Dot.

## System Components

### Orchiva Hub

- Synchronizes GitHub Issues.
- Manages development jobs and execution states.
- Assigns jobs to authorized Runners.
- Receives and stores execution results.
- Does not execute development tools locally.

### Orchiva Runner

- Runs as a separate .NET application on Windows.
- Retrieves available jobs from Hub.
- Claims jobs before execution.
- Executes Codex CLI, Git operations, builds, and tests.
- Creates Draft Pull Requests and reports results to Hub.

Runner implementation details belong to the separate Runner project.

## Automation Flow

1. A GitHub Issue is created.
2. Hub synchronizes eligible Issues into development jobs.
3. Runner retrieves available jobs using GET.
4. Runner requests a job claim using POST.
5. Hub atomically assigns the job.
6. Runner executes only after a successful claim response.
7. Runner reports completion or failure to Hub.
8. Successful implementation produces a Draft Pull Request.

Hub owns execution authorization and job state.

## MVP Scope

- GitHub Issue polling.
- Job persistence and state management.
- Runner polling and atomic job claiming.
- Execution result reporting.
- Single Runner with sequential execution.

Automatic merging, deployment, multi-agent coordination, and instruction database management are outside the initial scope.

## Development Environment

- Local: Hub, PostgreSQL, and Runner run on the development PC.
- Production: Hub and PostgreSQL run on the personal server; Runner runs on a separate Windows machine.

Environment-specific configuration belongs to `docs/agents/CONFIGURATION.md`.

## Related Documents

- `docs/agents/ARCHITECTURE.md` — Hub package structure.
- `docs/agents/API.md` — REST API contracts.
- `docs/agents/DEPLOYMENT.md` — Runtime and deployment.
- `docs/plans/` — Implementation plans.
- `docs/decisions/` — Technical decisions.