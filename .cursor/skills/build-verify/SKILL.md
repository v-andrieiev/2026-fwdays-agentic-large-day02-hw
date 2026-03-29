---
description: "Verifies that the project builds and tests pass after code changes. Use after implementing features, fixing bugs, or modifying dependencies."
---

# Skill: Build Verify

## When to use

After code changes that could affect compilation, tests, or lint.

Triggered by: "verify changes", "check build", "does it compile?", "run checks"

## Procedure

1. **Build shared packages** (dependency order matters):

   ```bash
   yarn build:packages
   ```

2. **Run TypeScript check**:

   ```bash
   yarn workspace @excalidraw/excalidraw tsc --noEmit
   ```

3. **Run formatting + lint check**:

   ```bash
   yarn test:other && yarn test:code
   ```

4. **Run tests**:

   ```bash
   yarn test --run
   ```

5. **Report results**:
   - Build: PASS/FAIL
   - TypeScript: error count
   - Lint: issue count
   - Tests: passed/failed/skipped

## On failure

- If build fails: check import paths and package dependencies
- If TypeScript fails: fix type errors before proceeding
- If tests fail: investigate whether it's a test issue or implementation issue
- Provide specific error messages and suggested fixes

## Constraints

- Run all steps in order — build must pass before tests
- Do not modify tests to make them pass unless the test is wrong
- Report all failures, don't just fix silently
