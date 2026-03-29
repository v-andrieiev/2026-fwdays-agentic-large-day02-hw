# AGENTS.md — Excalidraw AI Agent Baseline

## Project Overview
Excalidraw is an open-source collaborative whiteboard with a hand-drawn aesthetic. It's a **monorepo** with Yarn workspaces, built with React 19, TypeScript 5.9 (strict), and Vite 5.

## Project Structure
```
excalidraw-app/          — Full web application (excalidraw.com)
packages/
  excalidraw/            — Core React component library (@excalidraw/excalidraw)
    components/          — 156+ React components (colocated SCSS)
    actions/             — 100+ actions for state changes
    renderer/            — Canvas rendering pipeline (multi-layer)
    data/                — Persistence, import/export, reconciliation
    hooks/               — Custom React hooks
    types.ts             — Core types (AppState, etc.)
    editor-jotai.ts      — Jotai atom state setup
  element/               — Element types and operations
  math/                  — Geometry utilities (pure, no deps)
  common/                — Shared constants and types (no deps)
  utils/                 — Helper functions
```

## Development Workflow
```bash
yarn install             # Install dependencies
yarn build:packages      # Build shared packages (REQUIRED before app)
yarn start               # Dev server on :3001
yarn test                # Run Vitest tests
yarn fix                 # ESLint + Prettier auto-fix
```

## Architecture

### State Management
- Custom state via `actionManager` — **NOT** Redux, Zustand, MobX
- State type: `AppState` (packages/excalidraw/types.ts)
- State updates: `actionManager.dispatch()` ONLY
- Per-instance isolation via Jotai atoms

### Rendering
- Canvas-based via RoughJS (hand-drawn aesthetic)
- Multi-layer: static scene → interactive scene → new-element scene
- SVG export uses separate path

### Collaboration
- Real-time via WebSocket (socket.io-client)
- Conflict resolution: `reconcileElements()` in `packages/excalidraw/data/reconcile.ts`
- Backend: Firebase (auth, storage, Firestore)

### Action System
Each action has: `perform()`, `keyTest()`, `predicate()`
- 100+ registered actions
- All state modifications go through actions

## Constraints
- DO NOT suggest Redux, MobX, Zustand, or Recoil (Jotai is used internally for per-instance isolation — do not replace it)
- DO NOT suggest react-konva, fabric.js, pixi.js
- DO NOT add new npm dependencies without explicit approval
- DO NOT use `any` type — always provide proper types
- DO NOT use class components — functional + hooks only
- NEVER modify `restore.ts`, `manager.ts`, `types.ts` without approval

## Code Conventions
- TypeScript strict mode, no `any`
- Functional components with typed props
- PascalCase components, camelCase utilities
- Colocated tests and SCSS
- Vitest for testing (NOT Jest)
- AAA pattern in tests (Arrange/Act/Assert)

## Key Files for Onboarding
| Purpose | File |
|---------|------|
| App shell | `excalidraw-app/App.tsx` |
| Core component | `packages/excalidraw/components/App.tsx` |
| State types | `packages/excalidraw/types.ts` |
| Action system | `packages/excalidraw/actions/manager.ts` |
| Rendering | `packages/excalidraw/renderer/staticScene.ts` |
| Collaboration | `excalidraw-app/collab/Collab.tsx` |
| Data restore | `packages/excalidraw/data/restore.ts` |
