# Excalidraw — collaborative whiteboard (TypeScript/React monorepo)

## Commands
- `yarn install` — install deps
- `yarn build:packages` — build shared packages (run before app)
- `yarn start` — dev server on :3001
- `yarn test` — Vitest tests
- `yarn fix` — ESLint + Prettier

## Code style
- Functional components, no classes
- TypeScript strict mode, no `any`
- PascalCase for components, camelCase for utilities
- Colocated tests (`*.test.tsx`) and styles (`*.scss`)

## Architecture
- Custom state via `actionManager` (NOT Redux/Zustand/MobX/Recoil)
- Per-instance isolation via Jotai atoms (`editor-jotai.ts`) — do NOT replace with another state library
- Canvas rendering via RoughJS (NOT DOM-based, NOT react-konva/fabric.js/pixi.js)
- Monorepo: common → math → element → excalidraw → excalidraw-app
- Build order matters: `yarn build:packages` before `yarn start`

## Constraints
- No new npm deps without approval
- No direct state mutation — use actionManager.dispatch()
- No modifications to restore.ts, manager.ts, types.ts without approval
- Check packages/utils/ before adding external helpers
- Vitest for tests (not Jest)
