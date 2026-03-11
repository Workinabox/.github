# Workinabox — System Architecture

## Workspace

Workinabox is organized as a GitHub organization with one repo per major concern. In the local workspace, those repos live as siblings under a shared `workinabox/` directory.

## Repositories

### `.github`

Org-wide configuration. Contains agent instructions (`AGENTS.md`), this document, and shared GitHub configuration such as workflow templates and community health files.

### `dev`

The developer CLI. A Rust binary using Ratatui for the TUI. It is the center of gravity of the org — changes in other repos should be considered in terms of how they affect `dev`. It monitors the full org state and orchestrates synchronized releases across the sibling repos.

### `ui`

The web and desktop frontend. A Rust/WASM application using Leptos (CSR). Built and served via Trunk. The current implementation is a minimal shell and is intended to grow into the browser and desktop operator interface.

### `backend`

The backend service. A Rust application using Tokio for async execution. Package name `wiab`. It exposes HTTP endpoints for health and room discovery, a WebSocket signaling endpoint for real-time sessions, a mediasoup-based SFU, and optional local speech-to-text transcription.

### `app`

The mobile client. A React Native application written in TypeScript. It talks to the backend over HTTP and WebSocket, joins rooms, and publishes and consumes real-time audio via mediasoup-client and WebRTC.
