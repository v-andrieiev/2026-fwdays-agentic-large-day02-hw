---
description: "Updates the Memory Bank documentation with recent changes, ensuring all technical details are accurate and up to date. Use when the user asks to update the memory bank, sync documentation, or refresh project context."
---

# Skill: Memory Bank Update

## When to use
After significant code changes: new features, refactors, architecture changes, dependency updates, or completed milestones.

Triggered by: "update memory bank", "refresh project docs", "sync documentation"

## Procedure

1. **Identify what changed**:
   - Run `git diff --stat HEAD~5` to see recent changes
   - Ask user or check conversation for context

2. **Read relevant Memory Bank files** in `docs/memory/`:
   - `projectbrief.md` — project overview
   - `techContext.md` — tech stack and dependencies
   - `systemPatterns.md` — architecture patterns
   - `productContext.md` — features and UX
   - `activeContext.md` — current state
   - `progress.md` — completion status
   - `decisionLog.md` — architectural decisions

3. **For each changed area, update the matching file**:
   - New dependency? → update `techContext.md` (verify against monorepo build order: common → math → element → excalidraw)
   - Architecture change? → update `systemPatterns.md` (note actionManager patterns, canvas rendering pipeline)
   - New feature? → update `productContext.md` and `progress.md`
   - New decision? → add to `decisionLog.md` (note if protected files are affected: `restore.ts`, `manager.ts`, `types.ts`)
   - New active work? → update `activeContext.md`

4. **Cross-reference** — ensure links between docs are consistent

5. **Update `progress.md`** with current completion status

## Constraints
- Only update `docs/memory/` files
- Preserve existing format and structure
- Add timestamps to significant updates
- Do not remove historical entries — append new information
