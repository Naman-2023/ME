# MEE Core — Claude Code Context & Guidelines

This file provides system context, build instructions, and development standards for Claude Code and other AI coding assistants working on the MEE Rust codebase.

## Build and Test Commands

* **Build Workspace:** `cargo build`
* **Run Daemon:** `cargo run -p mee-daemon`
* **Run All Tests:** `cargo test`
* **Format Check:** `cargo fmt --check`
* **Code Linting:** `cargo clippy --all-targets -- -D warnings`

## Architecture Overview

* **`crates/mee-core`**: Core state-syncing engine and CRDT implementation.
* **`crates/mee-os`**: Native OS integration layer (system hooks, file watchers, clipboard API).
* **`crates/mee-daemon`**: Background system service managing real-time syncing.
* **`crates/mee-ffi`**: Foreign Function Interface bindings for client applications.

## Development Constraints & Style Guide

* **Memory & Safety:** Strict enforcement of `#![deny(unsafe_code)]` unless interacting directly with OS-level APIs in `mee-os`.
* **Async Runtime:** Powered by `tokio`. Prefer non-blocking I/O operations for all file system and network events.
* **Error Handling:** Use `thiserror` for library crates and `anyhow` for the daemon application. All OS API errors must be mapped to distinct `MeeError` variants.
* **Clipy Standards:** Fix all Clippy lints before opening a pull request. The build pipeline treats warnings as errors.
