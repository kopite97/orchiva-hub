# Development Workflow

## Mandatory Rule

Read this document before starting any task.

Determine the concerns affected by the task and read all applicable instructions.

Do not read every instruction document by default.

## Instruction Routing

- Project purpose, scope, Hub–Runner interaction → `../PROJECT_OVERVIEW.md`
- Domain terminology, model naming → `TERMINOLOGY.md`
- Architecture, packages, dependency boundaries → `ARCHITECTURE.md`
- REST API, DTO, Swagger, OpenAPI → `API.md`
- Environment variables, profiles, application settings → `CONFIGURATION.md`
- Java style, naming, Lombok, setter policy → `CONVENTIONS.md`
- Docker, Docker Compose, deployment, runtime → `DEPLOYMENT.md`
- Application, request, and error logging → `LOGGING.md`
- JPA, PostgreSQL, transactions, Flyway → `PERSISTENCE.md`
- Authentication, authorization, secrets → `SECURITY.md`
- Automated tests and verification → `TESTING.md`

## Before Implementation

1. Understand the request, expected behavior, and affected scope.
2. Read the applicable instruction files.
3. Inspect the existing implementation and project structure.
4. Review relevant plans and decisions.
5. Identify the smallest coherent change required.

Avoid unrelated refactoring, speculative features, and unnecessary abstractions.

## Planning

Before implementation, modification, refactoring, or debugging:

1. Read `../plans/AGENTS.md`.
2. Review `../plans/README.md`.
3. Create or update a plan according to the planning rules.
4. Keep new plans in `Planned` status until execution is authorized.
5. Change the plan to `Active` only after authorization.

Read-only analysis, documentation, and verification tasks do not require a new plan unless the planning rules specify otherwise.

### Execution Authorization

- Manual tasks require explicit user approval unless the user instructs otherwise.
- Automated tasks may proceed only when Orchiva Hub explicitly authorizes execution.
- A GitHub Issue alone does not constitute execution approval.
- Never self-approve a plan or exceed the authorized scope.
- Request additional approval when the required changes exceed that scope.

## Implementation

Follow all applicable instructions and the authorized task scope.

When applicable:

- Database schema changes → create a new Flyway migration.
- Configuration changes → follow `CONFIGURATION.md`.
- API changes → update API contracts and Swagger / OpenAPI.
- Security changes → verify authentication and authorization behavior.
- Domain naming changes → follow `TERMINOLOGY.md`.

For architectural changes, follow `../decisions/AGENTS.md`,
review `../decisions/README.md`, and record significant decisions.

Do not modify unrelated files or introduce unrequested features.

## Verification

After implementation:

1. Run applicable automated tests.
2. Build the application in the configured local environment.
3. Verify migrations and configuration changes when applicable.
4. For API changes, verify Swagger UI and `/v3/api-docs`.
5. Confirm that unrelated behavior and public contracts remain unchanged.

Use Docker Compose when required by the affected component or test environment.

Never remove, weaken, skip, or bypass tests merely to make verification pass.

Report any verification that could not be completed.

## Completion

A task is complete only when:

- The requested behavior is implemented.
- Applicable instructions are satisfied.
- Required verification succeeds.
- Relevant plans and documentation are updated when applicable.
- Results and limitations are reported.

For Orchiva-managed work, follow the authorized execution contract for result reporting and Draft PR creation.

Never merge, deploy, or modify protected branches without explicit authorization.

## Instruction Maintenance

- Keep each instruction focused on a single responsibility.
- Do not exceed 150 lines per instruction file.
- Do not move detailed rules into unrelated documents.
- If new rules exceed the document's scope or size limit,
  ask the user whether to create a separate instruction file.
- Never create additional instruction files without user approval.