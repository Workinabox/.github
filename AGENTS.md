# Workinabox — Organization-Wide Agent Instructions

## Workspace Structure

The workspace root is the organization folder. Each repo in the Workinabox GitHub org is a subdirectory:

``` md
workinabox/
  .github/    # org-wide defaults, templates, and this file
  dev/        # the dev CLI (Rust + Ratatui)
  ui/         # the frontend (Leptos/WASM)
  backend/    # the backend service (Rust/Tokio)
  app/        # the mobile app (React Native/TypeScript)
```

Agents should expect this layout. All repos are siblings under the same workspace root, so cross-repo file access is always available.

## General behavior

Be concise. Keep responses short. Do not pad answers with pleasantries or filler. Do not guess — if you are unsure, say so and verify before proceeding. Double-check facts, paths, and assumptions before presenting them. Do not suggest things unless explicitly asked. Always remember that you are an agent in a larger system, and your actions have consequences. Consider the impact of your actions on the whole system before proceeding. For example we should always check that workflows work.

When writing or editing Markdown files, always follow MD lint rules — in particular, surround headings with blank lines (MD022) and ensure consistent formatting throughout.

## Execution Discipline

Treat all implementation work as merge-bound production code unless the user explicitly asks for a prototype or spike. Do not use shortcuts, scaffolding, stand-ins, heuristics, fake fallbacks, or temporary implementations unless the user explicitly approves that exact tradeoff first.

If the design is incomplete, stop and surface the gap before writing code. Do not silently improvise missing policy, protocol, architecture, or runtime behavior. If a requested feature is too large for one coherent implementation step, decompose it first instead of collapsing unresolved parts into expedient code.

Respect the declared architecture. Follow DDD boundaries strictly: domain model and business rules in core, use cases and orchestration in app, adapters in inf, and composition only at the binary entrypoint. Do not hide domain behavior in infrastructure or application-layer convenience code.

Prefer typed errors in libraries and lower layers. Do not use `anyhow` deep inside library code unless the user explicitly approves it for that case. If a claim, fix, or diagnosis is not verified, say so plainly instead of presenting it as settled.

## Further Reading

Read `.github/SYSTEM_ARCHITECTURE.md` for details on the repository structure and system design. Read `.github/SOFTWARE_ARCHITECTURE.md` for coding paradigms, language boundaries, crate structure, and testing requirements.
