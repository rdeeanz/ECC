---
inclusion: auto
name: structure
description: Repository layout and organization conventions for the ECC project.
---

# Project Structure

## Top-Level Layout

```
ECC/
├── agents/              # 67 specialized subagents (Markdown) for Claude Code
├── skills/              # Canonical workflow surface — SKILL.md per skill
├── commands/            # Legacy slash-command compatibility shims (skills-first is preferred)
├── legacy-command-shims/# Opt-in archive for retired command shims
├── rules/               # Always-follow guidelines: common/ + per-language dirs
├── hooks/               # Trigger-based automations (hooks.json + subdirs)
├── scripts/             # Cross-platform Node.js tooling
│   ├── lib/             #   Shared utilities
│   ├── hooks/           #   Hook implementations
│   └── ci/              #   CI validators (agents, skills, rules, etc.)
├── src/llm/             # Python LLM package (cli, core, prompt, providers, tools)
├── ecc2/                # Rust control-plane prototype (alpha)
├── tests/               # Test suite (run-all.js + lib/ + hooks/)
├── mcp-configs/         # MCP server configurations
├── manifests/           # Install manifests for the selective installer
├── schemas/             # JSON schemas for validation
├── docs/                # Guides, release notes, translations
├── contexts/            # Dynamic system-prompt injection contexts
├── examples/            # Example project-level configs
├── scaffolds/           # Project scaffolding templates
├── integrations/        # Third-party integration configs
└── assets/              # Images, logos, dashboard assets
```

## Harness-Specific Directories

ECC ships pre-translated configs per harness at the repo root:
`.claude/`, `.claude-plugin/`, `.codex/`, `.codex-plugin/`, `.cursor/`, `.gemini/`,
`.opencode/`, `.zed/`, `.qwen/`, `.kimi/`, `.trae/`, `.codebuddy/`, `.openclaw/`,
`.hermes/`, `.github/` (Copilot), `.agents/` (Codex skills), and `.kiro/` (this Kiro setup).

## The `.kiro/` Directory

```
.kiro/
├── agents/     # Agents in both .json (CLI) and .md (IDE) formats
├── skills/     # SKILL.md workflows invocable via the / menu
├── steering/   # Always-on / conditional context (this dir)
├── hooks/      # IDE hooks (*.kiro.hook)
├── scripts/    # quality-gate.sh, format.sh
├── settings/   # MCP config examples
└── docs/       # Kiro-specific guides
```

## Conventions

- **Many small files over few large ones.** 200-400 lines typical, 800 max.
- **Organize by feature/domain, not by type.** High cohesion, low coupling.
- **Agents** are Markdown with YAML frontmatter (`name`, `description`, `tools`, `model`).
- **Skills** live in `skills/<name>/SKILL.md` with YAML frontmatter describing when to use them.
- **Steering** files use frontmatter with `inclusion: auto | fileMatch | manual`; `fileMatch` requires `fileMatchPattern`, and `auto` requires a `name`.
- **New workflow contributions land in `skills/` first**, not `commands/`.
- Root `AGENTS.md` is the universal cross-harness context file; per-harness dirs adapt it.
