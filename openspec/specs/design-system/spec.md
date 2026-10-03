# Design System

Source-of-truth specification for visual tokens, `@expo/ui` usage, and motion
policy. Pairs with [`DESIGN.md`](../../DESIGN.md), which is the implementation
reference. This file captures the *contract* — the rules every screen and
component MUST honor.

## Purpose

Make the design system enforceable at review time. Every UI change must consume
tokens defined here; any hard-coded color, font, or spacing value outside the
token map is a review failure.

## Requirements

### Requirement: Colors come from the token map

All UI MUST consume colors via the token map declared in `DESIGN.md` §2. The
system MUST NOT introduce a new color value (light or dark) without an `ADDED
Requirement` delta in this spec.

#### Scenario: A screen consumes tokens

- Given a screen renders a card
- When the developer writes the styles
- Then `backgroundColor` and `color` reference `theme.colors.surface` and
  `theme.colors.textPrimary` (or the equivalent token)
- And no hex literal appears in the component source

### Requirement: Typography uses the `text.*` scale

All text MUST use one of the typography tokens declared in `DESIGN.md` §3.
Custom font sizes or line-heights MUST NOT be introduced outside the scale.

#### Scenario: Adding a hero headline

- Given a screen needs a 32px headline
- When the developer writes the Text component
- Then the style references `theme.text.display`
- And the value 32 only exists in `DESIGN.md`, never in component source

### Requirement: Spacing follows the 4-point grid

All paddings, margins, and gaps MUST use values from the spacing scale
(`DESIGN.md` §4). The system MUST NOT use off-grid values like 13 or 17 pixels.

#### Scenario: Laying out a card

- Given a card with `padding: 16` inner spacing
- When the developer writes the styles
- Then the value is `theme.space[4]` (or equivalent token)
- And the literal `16` appears nowhere except `DESIGN.md`

### Requirement: Native UI comes from `@expo/ui`

The app MUST render UI through `@expo/ui` host trees when the universal API
covers the need. Raw `react-native` primitives MAY be used only when no
`@expo/ui` equivalent exists, and the deviation MUST be called out in the
change's `design.md`.

#### Scenario: Adding a button

- Given the developer needs a button
- When they choose the implementation
- Then `<Host><Button>...</Button></Host>` from `@expo/ui` is the default
- And a raw `<Pressable><Text>...</Text></Pressable>` only ships when no
  universal `@expo/ui` component fits

### Requirement: Motion respects `prefers-reduced-motion`

Every animation MUST short-circuit to a 0ms duration when
`useReducedMotion()` returns `true`. The system MUST NOT ship a Reanimated
worklet without that gate.

#### Scenario: User has reduced motion enabled

- Given the OS reports `prefers-reduced-motion: reduce`
- When the developer writes the animation
- Then the duration resolves to 0 and the final state is applied immediately

### Requirement: Accessibility is non-negotiable

Every interactive component MUST have a derived `accessibilityLabel`. Color
contrast MUST meet WCAG AA in both modes. Tap targets MUST be ≥ 44×44 (iOS) /
≥ 48×48 (Android).

#### Scenario: Reviewing a new button

- Given a developer submits a button component
- When a reviewer inspects it
- Then `accessibilityLabel` is derived from visible text
- And contrast against the background is ≥ 4.5:1
- And the hit area is at least 44×44

### Requirement: Dark mode ships by default

Every screen MUST render correctly in both light and dark modes. The app MUST
NOT ship a screen that assumes one mode without the other.

#### Scenario: Toggling the system theme

- Given the user toggles between light and dark in system settings
- When the app re-renders
- Then all screens swap tokens without a hard reload
- And no contrast, layout, or readability regression appears

## Non-goals

- Brand identity (logo system, wordmark) — owned by a separate `feat/brand-system` change.
- Marketing site styling.
- Per-screen `USE_SYSTEM_USER_INTERFACE_STYLE` overrides (we trust the system).