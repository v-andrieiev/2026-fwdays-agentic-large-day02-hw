---
description: "Explore and document an unfamiliar module or directory in the codebase"
---

# Explore Module

When the user provides a module path or name, investigate it thoroughly:

1. **List all files** in the target directory
2. **Read the main entry point** (index.ts, main file, or largest file)
3. **Identify key exports** — what does this module provide?
4. **Trace dependencies**:
   - What does this module import from other packages?
   - What other modules import from this one?
5. **Map the data flow**: entry point → processing → output
6. **Check for tests**: are there colocated test files?
7. **Excalidraw-specific checks**:
   - Which monorepo package does this module belong to? (common / math / element / excalidraw / excalidraw-app)
   - Does it use `actionManager.executeAction()` or mutate state directly?
   - Does it use Jotai atoms (`editor-jotai.ts`) for state isolation?
   - Does it involve canvas rendering via RoughJS?
   - Does it depend on protected files (`restore.ts`, `manager.ts`, `types.ts`)?

## Output format

Provide a structured summary:

### Module: [name]

- **Purpose**: one-line description
- **Key files**: list with brief descriptions
- **Exports**: main public API
- **Dependencies**: what it uses
- **Dependents**: what uses it
- **Test coverage**: yes/no, test file locations
- **Monorepo package**: which package in the build chain
- **State management**: actionManager.executeAction() / Jotai atoms / direct mutation
- **Rendering**: RoughJS canvas usage if any
- **Protected file deps**: restore.ts / manager.ts / types.ts if referenced
- **Notes**: anything unusual or important

**IMPORTANT**: This is a READ-ONLY exploration. Do NOT modify any files.
