# SKILLS.md — Agent Skills & Commands

> Cursor-specific AI capabilities for this project. See also: `CLAUDE.md` (Claude Code), `AGENTS.md` (generic AI agents).

## Skills (`.cursor/skills/`)

| Skill | Trigger phrases | Purpose |
|-------|----------------|---------|
| [build-verify](/.cursor/skills/build-verify/SKILL.md) | "verify changes", "check build", "does it compile?" | Build + TS + lint + test pipeline with failure triage |
| [codebase-explore](/.cursor/skills/codebase-explore/SKILL.md) | "investigate", "how does X work?", "explain module" | Read-only exploration of unfamiliar code areas |
| [memory-bank-update](/.cursor/skills/memory-bank-update/SKILL.md) | "update memory bank", "sync documentation" | Sync `docs/memory/` after significant changes |

## Commands (`.cursor/commands/`)

| Command | Purpose |
|---------|---------|
| [/build-verify](/.cursor/commands/build-verify.md) | Quick build verification (delegates to build-verify skill) |
| [/explore-module](/.cursor/commands/explore-module.md) | Deep read-only exploration of a module or directory |

## Rules (`.cursor/rules/`)

| Rule | Always Apply | Scope |
|------|-------------|-------|
| [architecture](/.cursor/rules/architecture.mdc) | Yes | `packages/excalidraw/**` |
| [conventions](/.cursor/rules/conventions.mdc) | Yes | `packages/**/*.{ts,tsx}` |
| [dependencies](/.cursor/rules/dependencies.mdc) | — | dependency management |
| [do-not-touch](/.cursor/rules/do-not-touch.mdc) | Yes | protected files |
| [negative-constraints](/.cursor/rules/negative-constraints.mdc) | — | anti-patterns & hallucination prevention |
| [testing](/.cursor/rules/testing.mdc) | — | Vitest conventions |
