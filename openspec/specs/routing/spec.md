# Routing

Source-of-truth specification for Expo Router file-based routing, navigation
patterns, and deep-link handling.

## Purpose

Define the rules every screen MUST follow when added under `src/app/`, plus the
navigation primitives the rest of the app composes from. Pairs with
[`DESIGN.md`](../../DESIGN.md) (screen visual language) and
[`AGENTS.md`](../../AGENTS.md) (workflow).

## Requirements

### Requirement: File-based routes live under `src/app/`

The app MUST use Expo Router with file-based routes rooted at `src/app/`. The
system MUST NOT add parallel route trees under different roots.

#### Scenario: A new screen is committed

- Given a developer adds a new file under `src/app/`
- When the Expo CLI rebuilds the bundle
- Then the route appears at the path matching the file name
- And `typedRoutes: true` (in `app.json`) MUST produce a typed route object

### Requirement: Root layout uses a single Stack

The root layout `src/app/_layout.tsx` MUST export a single `<Stack />` element
from `expo-router`. The Stack MUST NOT be replaced with a Tab or Drawer at the
root; tabs and drawers live in nested layouts.

#### Scenario: First launch

- Given the user opens the app
- When the root layout mounts
- Then a single Stack is rendered
- And the initial screen is `src/app/index.tsx`

### Requirement: Modal screens use Stack.Screen options

Screens that present modally MUST be declared with
`presentation: "modal"` or `presentation: "formSheet"` via `Stack.Screen` options
in a parent layout. The screen file MUST live next to its parent (e.g.,
`src/app/(main)/profile/edit.tsx` for an edit modal on the profile stack).

#### Scenario: Presenting a modal

- Given a screen is configured with `presentation: "formSheet"`
- When the user navigates to it
- Then the screen slides in as a sheet with the system dismiss gesture
- And the parent stack remains visible underneath

### Requirement: Deep links resolve via `app.json` scheme

The `app.json` `scheme` field MUST be a unique, lowercase string starting with
a letter. The system MUST NOT add deep-link paths outside the registered scheme
without updating this spec via an `ADDED Requirement` delta.

#### Scenario: External deep link

- Given `app.json` declares `scheme: "expocardtaxi"`
- When the OS opens `expocardtaxi://profile/123`
- Then Expo Router resolves it to `src/app/profile/[id].tsx` with `id="123"`

### Requirement: Tab navigation lives under a `(tabs)` group

Tab navigation, when added, MUST live under `src/app/(tabs)/` with one file
per tab (`index.tsx`, `explore.tsx`, etc.). A `<Tabs />` element MUST be
declared in `src/app/(tabs)/_layout.tsx`.

#### Scenario: A new tab is added

- Given a developer adds `src/app/(tabs)/settings.tsx`
- When the app rebuilds
- Then a "Settings" tab appears in the bottom bar
- And `/(tabs)/settings` becomes a typed route

## Non-goals

- Drawer navigation (out of scope; revisit if a future change requires it).
- Web-side custom routing (the project uses the same file-based tree for web).
- Server-driven routing (no remote config; rebuild ships new routes).