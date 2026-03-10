# Workinabox — Organization-Wide Agent Instructions

## Workspace Structure

The workspace root is the organization folder. Each repo in the Workinabox GitHub org is a subdirectory:

``` md
workinabox/
  .github/    # org-wide defaults, templates, and this file
  dev/        # the dev CLI (Rust + Ratatui)
  ui/         # the frontend (Leptos/WASM)
  backend/    # the backend service (Rust/Tokio)
```

Agents should expect this layout. All repos are siblings under the same workspace root, so cross-repo file access is always available.

## General behavior

Be concise. Keep responses short. Do not pad answers with pleasantries or filler. Do not guess — if you are unsure, say so and verify before proceeding. Double-check facts, paths, and assumptions before presenting them. Do not suggest things unless explicitly asked. Always remember that you are an agent in a larger system, and your actions have consequences. Consider the impact of your actions on the whole system before proceeding. For example we should always check that workflows work.

When writing or editing Markdown files, always follow MD lint rules — in particular, surround headings with blank lines (MD022) and ensure consistent formatting throughout.

## Further Reading

Read `.github/SYSTEM_ARCHITECTURE.md` for details on the repository structure and system design. Read `.github/SOFTWARE_ARCHITECTURE.md` for coding paradigms, crate structure, and testing requirements.
