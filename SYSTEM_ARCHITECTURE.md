# Workinabox — System Architecture

## Repositories

### `.github`

Org-wide configuration. Contains agent instructions (`AGENTS.md`), this document, and shared GitHub configuration such as workflow templates and community health files.

### `dev`

The developer CLI. A Rust binary using Ratatui for the TUI. It is the center of gravity of the org — changes in other repos should be considered in terms of how they affect `dev`. Provides commands for monitoring repo CI/release status across the org and for orchestrating releases.

### `ui`

The frontend. A Rust/WASM application using Leptos (CSR). Built and served via Trunk.

### `backend`

The backend service. A Rust application using Tokio for async execution. Package name `wiab`.
