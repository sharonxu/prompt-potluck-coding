# vibe-kanban AGENTS.md System Prompt

**Source:** [vibe-kanban/AGENTS.md](https://github.com/BloopAI/vibe-kanban/blob/main/AGENTS.md)  
**Date Added:** 2025-01-26  
**Contributed By:** @sharonxu

## Context

This is the `AGENTS.md` file from the [vibe-kanban](https://github.com/BloopAI/vibe-kanban) project (a Rust + TypeScript full-stack Kanban board application). This file is intended to guide AI coding agents when working within the repository by providing:

- Project structure and module organization
- Build, test, and development commands
- Coding style and naming conventions
- Testing guidelines
- Security and configuration tips

The vibe-kanban project is a notable example of a repository that includes explicit agent guidance files to improve AI-assisted coding workflows.

## How to Use

Place this file as `AGENTS.md` in your repository root (or adapt it for tools that use different filenames like `.cursor/rules`, `CLAUDE.md`, or `WARP.md`). AI coding assistants that recognize these files will use them as context when generating, refactoring, or reviewing code.

---

## Original AGENTS.md Content

```markdown
# Repository Guidelines

## Project Structure & Module Organization
- `crates/`: Rust workspace crates — `server` (API + bins), `db` (SQLx models/migrations), `executors`, `services`, `utils`, `deployment`, `local-deployment`.
- `frontend/`: React + TypeScript app (Vite, Tailwind). Source in `frontend/src`.
- `frontend/src/components/dialogs`: Dialog components for the frontend.
- `shared/`: Generated TypeScript types (`shared/types.ts`). Do not edit directly.
- `assets/`, `dev_assets_seed/`, `dev_assets/`: Packaged and local dev assets.
- `npx-cli/`: Files published to the npm CLI package.
- `scripts/`: Dev helpers (ports, DB preparation).

## Managing Shared Types Between Rust and TypeScript

ts-rs allows you to derive TypeScript types from Rust structs/enums. By annotating your Rust types with #[derive(TS)] and related macros, ts-rs will generate .ts declaration files for those types.
When making changes to the types, you can regenerate them using `npm run generate-types`
Do not manually edit shared/types.ts, instead edit crates/server/src/bin/generate_types.rs

## Build, Test, and Development Commands
- Install: `pnpm i`
- Run dev (frontend + backend with ports auto-assigned): `pnpm run dev`
- Backend (watch): `npm run backend:dev:watch`
- Frontend (dev): `npm run frontend:dev`
- Type checks: `npm run check` (frontend) and `npm run backend:check` (Rust cargo check)
- Rust tests: `cargo test --workspace`
- Generate TS types from Rust: `npm run generate-types` (or `generate-types:check` in CI)
- Prepare SQLx (offline): `npm run prepare-db`
- Local NPX build: `npm run build:npx` then `npm pack` in `npx-cli/`

## Coding Style & Naming Conventions
- Rust: `rustfmt` enforced (`rustfmt.toml`); group imports by crate; snake_case modules, PascalCase types.
- TypeScript/React: ESLint + Prettier (2 spaces, single quotes, 80 cols). PascalCase components, camelCase vars/functions, kebab-case file names where practical.
- Keep functions small, add `Debug`/`Serialize`/`Deserialize` where useful.

## Testing Guidelines
- Rust: prefer unit tests alongside code (`#[cfg(test)]`), run `cargo test --workspace`. Add tests for new logic and edge cases.
- Frontend: ensure `npm run check` and `npm run lint` pass. If adding runtime logic, include lightweight tests (e.g., Vitest) in the same directory.

## Security & Config Tips
- Use `.env` for local overrides; never commit secrets. Key envs: `FRONTEND_PORT`, `BACKEND_PORT`, `HOST`, optional `GITHUB_CLIENT_ID` for custom OAuth.
- Dev ports and assets are managed by `scripts/setup-dev-environment.js`.
```

## Notes

- This is an example of a well-structured agent guidance file for a full-stack Rust + TypeScript project
- Includes practical information about generated files (TypeScript types from Rust), which helps agents avoid editing files they shouldn't touch
- Covers the full development lifecycle: setup, testing, type checking, and deployment
- Can be adapted for other projects by replacing project-specific commands and structure with your own
