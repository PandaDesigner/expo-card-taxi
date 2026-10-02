# Build & Runtime

Source-of-truth specification for the build pipeline, runtime targets, and
verification commands. Pairs with [`AGENTS.md`](../../AGENTS.md) §Build & run.

## Purpose

Lock down which commands gate which changes, so verification is uniform
across every PR.

## Requirements

### Requirement: `bun` is the canonical package manager

The repo MUST use `bun` for install, scripts, and tooling. Lockfile is
`bun.lock`. `package-lock.json` and `yarn.lock` MUST NOT be committed.

#### Scenario: A new dependency is added

- Given a developer adds a package
- When they record the change
- Then `bun add <pkg>` (or `bun add -d <pkg>`) was used
- And only `bun.lock` was modified, never `package-lock.json`

### Requirement: TypeScript runs in strict mode

`tsconfig.json` MUST extend `expo/tsconfig.base` and enable `"strict": true`.
The system MUST NOT add files that fail `bunx tsc --noEmit`.

#### Scenario: A type error is committed

- Given a developer pushes a change with a type error in `src/`
- When CI (or local `bunx tsc --noEmit`) runs
- Then the build fails with a clear error pointing at the file
- And the change cannot land until it is fixed

### Requirement: Lint must be clean

`bun run lint` (which calls `expo lint`) MUST exit 0 on every PR. The system
MUST NOT disable a lint rule to make a check pass; the fix is in the code.

#### Scenario: A lint warning is committed

- Given a developer pushes code with a lint warning
- When the lint job runs
- Then the check fails and the PR blocks
- And the developer resolves it via `expo lint --fix` or by hand

### Requirement: Web smoke is the default verification target

Native UI changes MUST include screenshots from at least one target (iOS sim
preferred). Non-native changes MUST smoke-test on `bun run start --web` and
attach a screenshot or recording to the PR.

#### Scenario: Verifying a screen addition

- Given a developer adds a new screen
- When they request review
- Then the PR description includes screenshots for iOS, Android, or web
- And the chosen target's smoke command ran without errors

### Requirement: Ignored paths are not edited

Developers MUST NOT modify `.expo/`, `node_modules/`, `example/` (untracked
Expo Router reference template), or any other path covered by `.gitignore`.
Edits there are not persisted and confuse the build cache.

#### Scenario: An edit to `node_modules` is attempted

- Given a developer tries to patch a file in `node_modules`
- When they try to commit
- Then the file is ignored and not staged
- And the change should be replaced by a real patch via `patch-package`,
  a forked dependency, or by addressing the upstream issue

### Requirement: OpenSpec workflow governs non-trivial changes

Multi-file changes, new screens, and new components MUST go through
OpenSpec (`openspec/AGENTS.md`). Routing, theming, and native-module
boundary edits MUST also follow the workflow. Trivial fixes (typos,
single-line corrections) MAY bypass it.

#### Scenario: A feature is proposed

- Given a developer wants to add a "Favorites" tab
- When they start work
- Then `openspec/changes/feat/favorites-tab/` is created with
  `proposal.md`, `specs/`, `design.md`, `tasks.md`
- And the change ships through the proposal → spec → design → tasks →
  apply → verify → archive pipeline

### Requirement: Branch protection enforces GitHub Flow

`main` MUST be protected: PR required, linear history, no force-push, no
deletions, auto-delete source branch on squash merge. PRs that bypass these
rules MUST NOT merge.

#### Scenario: A direct push to main is attempted

- Given a developer pushes directly to `origin/main`
- When GitHub receives the push
- Then the push is rejected (force-push protection)
- And the developer is told to open a PR instead

## Non-goals

- Hosting / store distribution rules — owned by EAS-specific skills.
- Test infrastructure (no test runner yet) — owned by a future
  `feat/testing-foundation` change.