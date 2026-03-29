---
description: "Quick build + test + lint verification pipeline"
---

# Build Verify

> Canonical procedure: [`.cursor/skills/build-verify/SKILL.md`](../skills/build-verify/SKILL.md)

Run the following steps in order:

1. `yarn build:packages` — build shared packages (dependency order)
2. `yarn workspace @excalidraw/excalidraw tsc --noEmit` — TypeScript check
3. `yarn fix --dry-run` — lint check
4. `yarn test --run` — run tests

Report: Build / TypeScript / Lint / Tests — PASS or FAIL with details.

See the skill file for failure triage guidance.
