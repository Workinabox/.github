# Workinabox — Software Architecture

## Languages

Workinabox currently spans Rust and TypeScript:

- `backend`, `dev`, and `ui` are written in Rust.
- `app` is a React Native mobile client written in TypeScript.

## Paradigm

Domain-Driven Design (DDD). The backend domain is the center of gravity. Infrastructure and application concerns are always secondary to a clean, dependency-free domain model. User-facing clients should stay thin and align to the backend's domain language and protocol contracts.

## Crate Structure (backend)

The backend follows a strict three-layer crate split:

- **`wiab-core`** — The domain. Contains all business logic, domain models, and rules. Must have zero dependencies on other internal crates. External dependencies are limited to basic in-memory functionality (e.g. standard library, simple data structures). All code in this crate must be covered by tests.
- **`wiab-app`** — The application layer. Orchestrates use cases by combining domain logic with infrastructure interfaces. Depends on `wiab-core`.
- **`wiab-inf`** — The infrastructure layer. Implements persistence, external APIs, and other I/O. Depends on `wiab-core`. Must not contain business logic.

The root `wiab` binary wires everything together.

## Frontend Structure

- `ui` is the browser and desktop-facing Rust/WASM frontend.
- `app` is the mobile-facing React Native client.
- Frontends should avoid embedding business rules that belong in the backend domain. They are responsible for presentation, transport, device integration, and local interaction state.

## Dependency Rule

Dependencies only point inward:

```text
wiab (binary) → wiab-inf → wiab-core
```

`wiab-core` must never depend on `wiab-app` or `wiab-inf`.

## Testing

- All code in `wiab-core` must be tested. No exceptions.
- Code coverage is tracked and enforced in CI.
- `wiab-app` and `wiab-inf` are tested where practical, but coverage requirements are less strict.
- Client applications should at minimum keep their build and typecheck paths healthy.
- Tests live alongside the code they test using Rust's inline `#[cfg(test)]` modules, supplemented by integration tests in `tests/` where appropriate.

## Error Handling

Use `thiserror` for defining typed errors. Use `anyhow` only at the application boundary (binary entrypoints, CLI). Domain errors must be typed and explicit.
