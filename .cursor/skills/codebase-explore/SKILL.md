---
description: "Explores and documents an unfamiliar area of the Excalidraw codebase. Use when you need to understand how a module, component, or feature works before making changes."
---

# Skill: Codebase Explorer

## When to use

When you need to understand an unfamiliar area of the codebase.

Triggered by: "investigate", "how does X work?", "explain this module", "understand"

## Procedure

1. **Identify relevant directory/files** using @folder or @codebase search
2. **Read README or top-level comments** in the area
3. **Map the key files** and their responsibilities
4. **Check Excalidraw patterns**:
   - Does it use `actionManager.dispatch()` for state updates?
   - Is it part of canvas rendering (RoughJS usage)?
   - Which monorepo package does it belong to?
   - Does it depend on protected files (`restore.ts`, `manager.ts`, `types.ts`)?
   - Does it use Jotai atoms for state isolation?
5. **Trace data flow**: entry point → processing → output
6. **Identify dependencies**: what this module imports and what imports it
7. **Check for tests**: locate colocated test files (`.test.tsx`)
8. **Document findings** in a summary

## Output format

- **Summary**: purpose, key files, data flow, dependencies
- **List of related files** for deeper investigation
- **Known patterns**: how this module follows (or breaks) project conventions

## Constraints

- **READ-ONLY** — do not modify any files during exploration
- Focus on the specific area requested — don't explore the entire codebase
- Reference existing documentation in `docs/` if available
