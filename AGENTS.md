# Card Taxi — Agent Instructions

> Read this file BEFORE editing code. Pair with [`openspec/AGENTS.md`](openspec/AGENTS.md)
> for spec-driven workflow and [`.atl/skills-applicability.md`](.atl/skills-applicability.md)
> for which `SKILL.md` to load per task type.

## What this project is

**Card Taxi** is an Expo Router app built on `@expo/ui` native components (SwiftUI on
iOS, Jetpack Compose on Android). The repo is currently in bootstrap phase: minimal
Stack layout, no screens beyond a placeholder `index.tsx`. Use this file as the
single source of truth for stack, conventions, and AI-driven development rules.

## Stack

| Layer | Choice |
| --- | --- |
| Runtime | Expo SDK 57, React 19.2, React Native 0.86 |
| Routing | Expo Router (`expo-router/entry`, typed routes, React Compiler on) |
| UI primitives | `@expo/ui` (`Host` + universal `Button`/`Text`/etc., platform-specific SwiftUI / Compose) |
| Animation | Reanimated 4 + Worklets |
| Gestures | `react-native-gesture-handler`, `react-native-screens` |
| Icons | `expo-symbols` (SF Symbols on iOS, Material on Android) |
| TypeScript | strict mode, paths `@/*` → `./src/*`, `@/assets/*` → `./assets/*` |
| Package manager | `bun` (preferred), `npm` works |
| Platforms | iOS, Android, Web (`expo start --web`) |

## Repository layout

```text
expo-card-taxi/
├── AGENTS.md               ← you are here
├── DESIGN.md               ← design system + @expo/ui mapping
├── CONTRIBUTING.md         ← GitHub Flow rules for humans
├── README.md               ← project overview (replace scaffolded copy)
├── app.json                ← Expo config (splash, icons, plugins)
├── src/
│   └── app/                ← Expo Router file-based routes
│       ├── _layout.tsx     ← root Stack
│       └── index.tsx       ← placeholder home
├── assets/                 ← images, icon set, splash
├── openspec/               ← Spec-Driven Development workflow
│   ├── AGENTS.md           ← OpenSpec-specific workflow rules
│   ├── config.yaml         ← stack, rules per phase, testing
│   ├── specs/              ← source-of-truth capabilities
│   └── changes/            ← active + archive of changes
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── .atl/
│   ├── skill-registry.md   ← auto-generated index of available SKILL.md
│   └── skills-applicability.md ← which skills to load per task
└── .pi/                    ← OpenSpec pi integration (slash commands + skills)
```

## Build & run commands

```bash
bun install                       # install deps
bun run start                     # expo start (interactive target picker)
bun run ios                       # iOS simulator
bun run android                   # Android emulator
bun run web                       # web (Metro + static export)
bun run lint                      # expo lint
bunx tsc --noEmit                 # typecheck only
```

> Web smoke is the fastest verification target. Prefer it when the change does not
> touch native-only APIs (gestures, haptics, native modules).

## Development rules for AI agents

### Read before you write

1. **OpenSpec first.** If the task is more than a single-line tweak, a new screen,
   a component, a route, or any change that touches ≥2 files, **start a change** in
   `openspec/changes/<change-id>/`. Read `openspec/AGENTS.md` for the workflow.
2. **Load the right skills.** See `.atl/skills-applicability.md`. Do not load
   skills blindly — load the ones relevant to the task before editing code.
3. **Read the design system.** Any UI change must respect tokens defined in
   `DESIGN.md`. Hard-coded colors, spacing, or fonts outside the token map are a
   review failure.

### Hard rules

- **No edits to OpenSpec scaffolded content.** Do not modify `.pi/prompts/opsx-*.md`
  or `.pi/skills/openspec-*/SKILL.md`. Those belong to the OpenSpec install; modify
  the install or the OpenSpec config instead.
- **No edits to ignored paths.** `.expo/`, `node_modules/`, `example/` (untracked
  Expo Router reference template). The `example/` folder generates pre-existing
  TypeScript errors under `tsconfig.include: **/*.ts`; those are not regressions.
- **No force-push to `main`.** Branch protection forbids it.
- **No merge commits.** Use squash or rebase merges to keep linear history.
- **Conventional Commits.** `feat(scope):`, `fix(scope):`, `chore:`, `docs:`,
  `refactor:`, `perf:`, `test:`. Branch prefix mirrors the commit type.
- **One PR per purpose.** Refactors bundled only when they share the same
  subsystem; otherwise split into separate PRs.

### Verification

Before declaring a task done:

1. `bunx tsc --noEmit` — clean.
2. `bun run lint` — clean.
4. Smoke test on at least one target. Native UI changes need iOS sim + Android
   emulator + web screenshots attached to the PR.
3. Walk every scenario from the change's delta spec (see `openspec/AGENTS.md`).
4. Update `openspec/changes/<change-id>/tasks.md` checkboxes as you go.

## When to ask the human

Stop and ask instead of guessing when:

- A task affects routing structure (new tabs, deep links, modal stacks).
- A task introduces a new external dependency (npm install beyond `bun add`).
- A spec scenario is ambiguous or contradicts existing behavior.
- Verification fails twice on the same root cause.
- The change would touch OpenSpec scaffolded files or branch protection settings.

## Pointers

- [`openspec/AGENTS.md`](openspec/AGENTS.md) — spec-driven workflow
- [`DESIGN.md`](DESIGN.md) — design system, tokens, `@expo/ui` mapping
- [`.atl/skills-applicability.md`](.atl/skills-applicability.md) — SKILL.md routing
- [`CONTRIBUTING.md`](CONTRIBUTING.md) — GitHub Flow rules for human contributors