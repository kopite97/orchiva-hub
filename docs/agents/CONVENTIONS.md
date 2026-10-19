# Coding Conventions

## Scope

This document defines Java coding conventions for Orchiva Hub (Spring Boot).

Follow standard Java and Spring Boot conventions.

Prefer simple, readable, and maintainable code over unnecessary abstractions.

## Lombok

Use Lombok actively to reduce boilerplate code.

Prefer the following annotations when appropriate:

- `@Getter` — Read-only property access.
- `@RequiredArgsConstructor` — Constructor generation and dependency injection.
- `@NoArgsConstructor` — Framework-required constructors.
- `@AllArgsConstructor` — Full-argument constructors.
- `@Builder` — Object construction with multiple parameters.
- `@Slf4j` — Logger declaration.

Rules:

- Avoid `@Data` and unrestricted class-level `@Setter`.
- Do not manually implement boilerplate already handled appropriately by Lombok.
- Use only the annotations required by each class.
- Follow `PERSISTENCE.md` for JPA entity-specific Lombok restrictions.

## Setter Policy

Avoid setters by default.

Prefer:

- Constructor initialization.
- Builder-based creation.
- Explicit domain methods.
- Purpose-specific update methods.

Use meaningful methods such as `changeStatus(...)` or `updateName(...)` instead of generic setters.

Allow setters only when unrestricted mutation is explicitly appropriate.

## Dependency Injection

- Use constructor injection.
- Prefer `@RequiredArgsConstructor` with `final` dependencies.
- Do not use field injection with `@Autowired`.
- Avoid unnecessary dependency injection abstractions.

## Immutability

- Prefer `final` for values and dependencies that should not change.
- Prefer Java `record` for immutable DTOs when appropriate.
- Avoid mutable shared state without a clear requirement.
- Do not introduce unnecessary state into Spring singleton components.

## Naming

Use descriptive names that express intent and responsibility.

- Classes, interfaces, records → `PascalCase`
- Methods, fields, variables → `camelCase`
- Constants → `UPPER_SNAKE_CASE`
- Packages → lowercase
- Boolean methods → `is`, `has`, or `can` prefixes when appropriate

Avoid vague names such as `Util`, `Helper`, `Manager`, or `Common` without a clearly defined responsibility.

Follow `TERMINOLOGY.md` for domain-specific naming.

## General Rules

- Keep classes and methods focused on a single responsibility.
- Prefer early returns over deeply nested conditions.
- Use clear control flow rather than unnecessarily complex expressions.
- Use modern Java features when they improve readability.
- Remove unused imports, variables, and dead code.
- Do not leave commented-out implementation code.
- Add comments to explain intent or non-obvious reasoning, not obvious behavior.
- Follow the existing project formatting and style.
- Avoid unrelated formatting changes or refactoring.
