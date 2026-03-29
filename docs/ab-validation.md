# A/B Validation: architecture.mdc Rule

## Test Setup

- **Rule tested**: `.cursor/rules/architecture.mdc`
- **Test prompt**: "Create a new React component for displaying element coordinates. It should show: type, position (x,y), dimensions (w,h), rotation."
- **Tool**: Cursor AI (Agent mode)

---

## Test A — Rule ON (architecture.mdc active, alwaysApply: true)

### AI Response Summary
The AI generated a component that:
- Used `actionManager.dispatch()` for any state updates
- Referenced `AppState` from `packages/excalidraw/types.ts`
- Used existing type `ExcalidrawElement` for element properties
- Created a functional component with typed props (`ElementCoordinatesProps`)
- Did NOT suggest any external state management library
- Placed the component in `packages/excalidraw/components/` with colocated SCSS
- Used existing utility functions from `packages/math/` for coordinate calculations

### Key code patterns observed
```typescript
// Correct: uses project types
import type { ExcalidrawElement } from "@excalidraw/element/types";
import type { AppState } from "../types";

interface ElementCoordinatesProps {
  element: ExcalidrawElement;
  appState: AppState;
}

// Correct: functional component, no class
const ElementCoordinates = ({ element, appState }: ElementCoordinatesProps) => {
  // Reads from element properties directly (read-only display)
  const { x, y, width, height, angle, type } = element;
  // ...
};
```

---

## Test B — Rule OFF (architecture.mdc renamed to .bak)

### AI Response Summary
The AI generated a component that:
- Used `useState` for local component state (acceptable for display-only)
- **Suggested `zustand` store** for sharing coordinates across components
- Used generic React types instead of project-specific `ExcalidrawElement`
- Created inline styles instead of colocated SCSS
- Did NOT reference `actionManager` or `AppState`
- Suggested adding a new `@types/coordinates` package

### Key code patterns observed
```typescript
// Incorrect: uses generic types instead of project types
interface Coordinates {
  x: number;
  y: number;
  width: number;
  height: number;
  rotation: number;
  type: string;  // string instead of element type union
}

// Incorrect: suggests Zustand for state sharing
import { create } from 'zustand';
const useCoordinatesStore = create<CoordinatesState>((set) => ({
  selectedElement: null,
  // ...
}));
```

---

## Comparison

| Aspect | Test A (Rule ON) | Test B (Rule OFF) |
|--------|-----------------|-------------------|
| **State management** | Uses existing `AppState` + `actionManager` | Suggests `zustand` store |
| **Types** | `ExcalidrawElement`, `AppState` from project | Generic custom interfaces |
| **Component style** | Functional + typed props | Functional but generic types |
| **File structure** | Colocated in `packages/excalidraw/components/` | Flat in src/ |
| **Dependencies** | No new deps | Suggests `zustand`, `@types/coordinates` |
| **Styling** | SCSS colocated file | Inline styles |
| **Project awareness** | References real project structure | Generic React patterns |

## Conclusion

The `architecture.mdc` rule **effectively prevents** the AI from:
1. Suggesting external state management libraries (Zustand, Redux)
2. Using generic types instead of project-specific ones
3. Adding unnecessary npm dependencies
4. Ignoring project file structure conventions

**The rule is validated** — it significantly improves AI output quality for this project.
The most critical impact is preventing Zustand/Redux suggestions, which would conflict with the custom `actionManager` pattern.
