---
inclusion: auto
name: product
description: Product overview of the Everything Claude Code (ECC) project — what it is, who it serves, and its core value.
---

# Product Overview

**Everything Claude Code (ECC)** is a harness-native agent operating system for AI-assisted software engineering. It is distributed as `ecc-universal` (npm) and as a Claude Code plugin (`ecc@ecc`), and works across multiple agent harnesses: Claude Code, Codex, Cursor, OpenCode, Gemini, Zed, GitHub Copilot, Kiro, and others.

## What It Provides

- **Agents** — Specialized subagents for planning, review, build fixing, and language-specific work (Go, Python, Rust, Java, Kotlin, C++, Swift, TypeScript, Django, PyTorch/ML, etc.).
- **Skills** — On-demand workflows and domain knowledge (TDD, security review, API design, framework patterns, research, deployment, and more).
- **Hooks** — Trigger-based automations (lint on save, typecheck on edit, secret detection, session memory persistence, quality gates).
- **Rules / Steering** — Always-follow guidelines for coding style, security, testing, and per-language conventions.
- **MCP configurations** — Curated Model Context Protocol server setups.
- **Control-plane tooling** — CLI (`ecc`), install/uninstall pipeline, session/state tracking, and an alpha Rust control plane (`ecc2/`).

## Core Value

ECC packages battle-tested agentic workflows into reusable, cross-harness configuration so teams get consistent, high-quality, security-first AI assistance without rebuilding prompt scaffolding for each tool.

## Guiding Principles

1. **Agent-first** — Delegate domain tasks to specialized agents.
2. **Test-driven** — Tests before implementation, 80%+ coverage.
3. **Security-first** — Validate all inputs, never hardcode secrets.
4. **Immutability** — Prefer new objects over mutation.
5. **Plan before execute** — Plan complex work before writing code.
6. **Skills-first surface** — `skills/` is the canonical workflow surface; `commands/` is a legacy compatibility layer.

## Distribution & Safety

Install only from official channels (GitHub `affaan-m/ECC`, npm `ecc-universal` / `ecc-agentshield`, the `ecc@ecc` plugin, and ecc.tools). Do not stack multiple install methods. The repo is MIT-licensed; ECC Pro (hosted GitHub App) and sponsors fund ongoing work.
