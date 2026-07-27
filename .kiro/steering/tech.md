---
inclusion: auto
name: tech
description: Technology stack, tooling, and common commands for the ECC project.
---

# Technology Stack

ECC is primarily a **configuration and tooling distribution** (Markdown assets + cross-platform scripts) rather than a single application.

## Languages & Runtimes

- **Node.js (>=18)** — Primary tooling language. All installer, hook, catalog, and control-pane scripts are cross-platform Node.js under `scripts/`.
- **Python (3.x)** — Desktop dashboard (`ecc_dashboard.py`, Tkinter) and the `src/llm/` package (CLI, core, prompt, providers, tools). Config in `pyproject.toml`.
- **Rust** — Alpha control-plane prototype in `ecc2/` (Cargo, pinned via `rust-toolchain.toml`).
- **Shell / PowerShell** — Installers (`install.sh`, `install.ps1`) and quality scripts.
- **Markdown** — Agents, skills, rules, steering, and docs (the bulk of the repo).

## Package Management

- npm is the reference package manager; `yarn@4.9.2` is pinned via `packageManager`. Lockfiles for npm and yarn are present.
- ECC auto-detects the user's package manager (npm, pnpm, yarn, bun).

## Key Dependencies

- Runtime: `@iarna/toml`, `ajv` (JSON schema validation), `sql.js` (SQLite state store).
- Dev: `eslint`, `markdownlint-cli`, `typescript`, `c8` (coverage), `@types/node`.

## Common Commands

```bash
# Full validation + test suite
npm test

# Coverage (enforces 80% lines/functions/statements, 79% branches)
npm run coverage

# Lint (ESLint + markdownlint)
npm run lint

# Catalog checks / sync
npm run catalog:check
npm run catalog:sync

# Command registry
npm run command-registry:check

# Run only the JS test harness
node tests/run-all.js

# Harness / operator tooling
npm run harness:audit
npm run operator:dashboard
npm run security:ioc-scan

# Desktop dashboard
npm run dashboard        # Python/Tkinter
npm run dashboard:web    # Node web dashboard

# CLI entry points (via bin)
ecc consult "security reviews" --target claude
```

## Testing & Quality

- Tests live in `tests/` (run via `node tests/run-all.js`) plus CI validators under `scripts/ci/` (agents, commands, rules, skills, hooks, install manifests, unicode safety, personal paths).
- Minimum coverage target: **80%**.
- Conventional commits (`feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`, `perf:`, `ci:`).

## Notes

- Do NOT add a `"hooks"` field to `.claude-plugin/plugin.json` (causes duplicate-hook errors; enforced by a regression test).
- ECC ships exactly one default MCP connector (`chrome-devtools`); everything else is opt-in.
