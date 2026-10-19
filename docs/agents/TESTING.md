# Testing Guidelines

## Scope

This document defines automated testing and verification rules for Orchiva Hub.

Use an isolated Docker Compose environment for automated tests.

Prioritize correctness, regression prevention, and reliable verification.

## Testing Principles

- Derive test cases from requirements and acceptance criteria.
- Cover normal behavior, edge cases, and expected failures.
- Test observable behavior rather than implementation details.
- Write tests for behavior that can fail meaningfully.
- Keep tests independent, deterministic, and repeatable.
- Avoid trivial tests and unnecessary mocking.
- Do not add tests solely to increase code coverage.

## Test Strategy

Use the smallest test scope that reliably verifies behavior.

- Unit tests → Business logic, validation, and state transitions.
- Controller tests → HTTP contracts, status codes, and validation.
- Repository tests → Persistence queries and database constraints.
- Integration tests → Transactions, concurrency, and component interactions.
- End-to-end tests → Complete workflows when applicable.

Prioritize tests for Job registration, duplicate prevention, atomic claiming, execution states, and failure handling.

Verify database concurrency with actual PostgreSQL transactions, not mocks alone.

## Test Environment

All automated tests must run through the dedicated `compose.test.yml`.

```text
Docker Compose (Test)
├── test
│   └── Java 21 + Gradle Wrapper
│       └── Build / Tests
└── postgres-test
    └── Isolated PostgreSQL
```

- Run the application tests inside the `test` container.
- Use a dedicated PostgreSQL service, database, and temporary volume.
- Isolate test containers, networks, and volumes from other environments.
- Use a dedicated Compose project name for each test run.
- Wait for PostgreSQL healthcheck before executing tests.
- Initialize the test schema using Flyway.
- Never access development or production databases during automated tests.
- Mock or stub external APIs unless explicitly testing integration behavior.
- Use authorized test resources for real external integration tests.

## Test Execution

- Use the Gradle Wrapper for test execution.
- Run applicable tests and the application build.
- Return the actual Gradle exit code from the test container.
- Fail verification when required tests, builds, or migrations fail.
- Do not silently ignore test failures.

Example commands:

```bash
docker compose -p orchiva-test -f compose.test.yml run --build --rm test
docker compose -p orchiva-test -f compose.test.yml down -v --remove-orphans
```

These commands are illustrative. Use a unique project name when multiple runs may overlap.

The test execution script must preserve the test exit code and execute cleanup even when tests fail or are interrupted.

## Test Cleanup

- Remove test containers, networks, and temporary volumes after execution.
- Remove temporary files and generated test data.
- Perform cleanup after both successful and failed runs.
- Retain test reports only in an explicitly configured output directory.
- Never delete source files or committed test code.
- Never remove development or production containers, networks, or volumes.
- Do not use external or shared Docker volumes for temporary test data.

## Verification

After implementation:

1. Run tests covering the changed behavior.
2. Run relevant regression tests.
3. Verify database integration and concurrency when applicable.
4. Build the application successfully.
5. Verify Swagger / OpenAPI when APIs change.
6. Report test results and any unverified behavior.

Never remove, weaken, skip, or bypass tests merely to make verification pass.

Fix implementation defects rather than changing correct test expectations.

## Completion Criteria

A task is verified only when:

- Acceptance criteria are satisfied.
- Required automated tests pass.
- The application builds successfully.
- Relevant integration behavior is verified.
- No known critical defects remain.
- Verification results and limitations are reported.

Passing tests does not authorize merging or deployment.

Follow `WORKFLOW.md` for task completion and approval requirements.