# Architecture Guidelines

## Scope

This document defines the package structure and dependency boundaries of Orchiva Hub (Spring Boot).

Use a feature-oriented layered architecture.

- Project scope and system interactions → [PROJECT_OVERVIEW.md](../PROJECT_OVERVIEW.md)
- REST API contracts → `API.md`
- Domain terminology → `TERMINOLOGY.md`

## Package Structure

Organize packages by feature, with responsibility-specific subpackages.

```text
<base-package>/
├── global/
│   ├── config/
│   └── exception/
├── job/
│   ├── controller/
│   ├── service/
│   ├── repository/
│   ├── entity/
│   └── dto/
├── github/
│   ├── config/
│   ├── client/
│   ├── service/
│   ├── scheduler/
│   └── dto/
└── runner/
    ├── controller/
    ├── service/
    └── dto/
```

- Create only the packages required by implemented features.
- Place implementation classes in responsibility-specific subpackages, not feature roots.
- Do not create speculative packages or unnecessary abstraction layers.

## Feature Responsibilities

- `job` → Job registration, lifecycle, state management, and persistence.
- `github` → GitHub API integration and Issue synchronization.
- `runner` → Runner-facing REST APIs and communication.
- `global` → Shared configuration, exceptions, and cross-cutting infrastructure.

Keep business logic within the feature that owns it.

## Layer Responsibilities

- `controller` → HTTP requests, validation, and responses.
- `service` → Business logic, orchestration, and transaction boundaries.
- `repository` → Database access only.
- `entity` → JPA entities and persistence state.
- `dto` → Request, response, and transfer objects.
- `config` → Spring configuration.
- `client` → External API communication.
- `scheduler` → Scheduled triggers that delegate to services.

## Dependency Rules

```text
Controller → Service → Repository
                     → External Client
```

- Controllers must not access repositories or external clients directly.
- Features must communicate through the owning feature's services.
- Do not access another feature's repositories or entities directly.
- Never expose JPA entities through REST APIs.
- Use constructor injection and avoid circular dependencies.
- Keep feature-specific logic out of `global`.

## Change Principles

- Prefer the smallest coherent change.
- Preserve feature ownership and dependency direction.
- Avoid unrelated refactoring and unnecessary interfaces.
- Record significant architectural decisions in `docs/decisions/`.
