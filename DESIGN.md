# Card Taxi — Design System

> Single source of truth for visual design and `@expo/ui` usage. Any UI change
> that hard-codes a color, font, or spacing value not defined here is a review
> failure. Pair with [`AGENTS.md`](AGENTS.md) for the development workflow.

## 1. Principles

1. **Native feel first.** The app uses `@expo/ui` so iOS gets SwiftUI and Android
   gets Jetpack Compose. Do not reach for raw `react-native` primitives when an
   `@expo/ui` host tree gives the same result.
2. **One component, two render trees.** Prefer the **universal** API
   (`@expo/ui` root) unless the design demands platform-specific behaviour
   (`@expo/ui/swift-ui` for iOS-only, `@expo/ui/jetpack-compose` for Android-only).
3. **Tokens, not magic numbers.** Spacing, colors, and typography are tokens.
   Components consume tokens; they never read a hard-coded value.
4. **Motion is purposeful.** Reanimated 4 worklets for transitions, gestures, and
   micro-interactions. Disable for `prefers-reduced-motion`.
5. **Dark mode by default.** Both light and dark palettes ship; the user picks.
   We never assume "white background" without an explicit token override.

## 2. Color tokens

All colors live as Expo constants (`expo-constants` / app config) and surface via
a `useThemeColor()` hook (defined under `src/hooks/`). Wireframe values below are
the **initial palette** — replace during the first `feat/theme-system` change.

| Token | Light | Dark | Usage |
| --- | --- | --- | --- |
| `--color-bg` | `#FFFFFF` | `#0B0B0E` | App background |
| `--color-surface` | `#F7F7F9` | `#15151A` | Cards, sheets |
| `--color-surface-elevated` | `#FFFFFF` | `#1E1E25` | Modals, popovers |
| `--color-border` | `#E5E5EA` | `#2A2A33` | Hairline dividers |
| `--color-text-primary` | `#0B0B0E` | `#FAFAFA` | Body, headings |
| `--color-text-secondary` | `#5C5C66` | `#A0A0AA` | Labels, captions |
| `--color-text-muted` | `#8A8A93` | `#6B6B75` | Placeholders |
| `--color-brand` | `#208AEF` | `#3FA3FF` | Primary CTA, links |
| `--color-brand-pressed` | `#1869BD` | `#2A82D9` | Pressed state |
| `--color-success` | `#1FA66B` | `#3FCB8E` | Confirmations |
| `--color-warning` | `#E69B00` | `#FFB835` | Warnings |
| `--color-danger` | `#D6361A` | `#F25636` | Destructive |

> **Until `feat/theme-system` lands:** use the existing `app.json` splash
> background `#208AEF` and adaptive icon background `#E6F4FE` as the de-facto
> brand colors.

### Mapping to `@expo/ui`

```tsx
// Universal — recommended
import { Host, Text } from "@expo/ui";

<Host style={{ backgroundColor: theme.colors.bg }}>
  <Text color={theme.colors.textPrimary}>Hello</Text>
</Host>
```

```tsx
// iOS-only — SwiftUI
import { Host, Text } from "@expo/ui/swift-ui";

// Android-only — Compose
import { Host, Text } from "@expo/ui/jetpack-compose";
```

## 3. Typography

Use the **system font** by default. Only switch to a custom font when a screen
needs branded display type. Expo Router projects typically load custom fonts via
`expo-font` and gate the splash until loaded.

| Token | Size / line-height | Weight | Usage |
| --- | --- | --- | --- |
| `text.display` | 32 / 38 | 700 | Hero headlines |
| `text.title1` | 24 / 30 | 700 | Screen titles |
| `text.title2` | 20 / 26 | 600 | Section titles |
| `text.body` | 16 / 22 | 400 | Body copy |
| `text.bodyEmphasis` | 16 / 22 | 600 | Emphasized body |
| `text.label` | 14 / 18 | 600 | Field labels, button text |
| `text.caption` | 12 / 16 | 400 | Captions, helper text |
| `text.mono` | 14 / 20 | 500 | Codes, IDs, technical strings |

## 4. Spacing scale

4-point grid. All spacing values come from this scale; never use `padding: 13`.

| Token | Value | Use case |
| --- | --- | --- |
| `space.0` | 0 | Reset |
| `space.1` | 4 | Tight stacks |
| `space.2` | 8 | Default inline gap |
| `space.3` | 12 | Card inner padding |
| `space.4` | 16 | Screen horizontal padding |
| `space.5` | 20 | Section gap |
| `space.6` | 24 | Section separation |
| `space.8` | 32 | Hero spacing |
| `space.10` | 40 | Top of page / major break |
| `space.12` | 48 | Bottom safe area buffer |

## 5. Radius

| Token | Value | Use case |
| --- | --- | --- |
| `radius.none` | 0 | Tables, raw rectangles |
| `radius.sm` | 6 | Tags, chips |
| `radius.md` | 12 | Cards, buttons |
| `radius.lg` | 20 | Sheets, large cards |
| `radius.pill` | 9999 | Avatars, status dots |

## 6. Elevation

Prefer **border + subtle surface tint** over heavy shadows on iOS; use Compose
`tonalElevation` on Android for the equivalent. If you reach for a drop shadow, it
MUST be one of these tokens:

| Token | iOS shadow | Android elevation |
| --- | --- | --- |
| `elev.0` | none | `0.dp` |
| `elev.1` | `0 1 2 rgba(0,0,0,0.06)` | `1.dp` |
| `elev.2` | `0 4 12 rgba(0,0,0,0.10)` | `4.dp` |
| `elev.3` | `0 8 24 rgba(0,0,0,0.14)` | `8.dp` (modals) |

## 7. Iconography

- Use **`expo-symbols`** for SF Symbols (iOS) and Material symbols (Android).
- Iconography is monochrome and inherits `color-text-primary` by default.
- Available sizes: `16`, `20`, `24`, `32`. Use 24 as the default.
- Custom icons live in `assets/icons/svg/`, exported as React components, never
  rasterized past `@3x`.

## 8. Components (the ones we'll standardize on)

The first iteration builds from `@expo/ui` universal primitives; custom screens
compose them in `src/components/` once a real need shows up.

| Need | Use |
| --- | --- |
| Buttons | `@expo/ui` `Button` (universal) — variants: `primary`, `secondary`, `ghost`, `destructive` |
| Text input | `@expo/ui` `TextField` (universal) |
| Toggle | `@expo/ui` `Switch` (universal) |
| List / scroll | `@expo/ui` `List` (universal) inside a `Host` |
| Modal | Expo Router `Stack.Screen options={{ presentation: "modal" }}` |
| Sheet | Expo Router `Stack.Screen options={{ presentation: "formSheet", sheetAllowedDetents: [0.5, 1] }}` |
| Tabs | Expo Router `Tabs` (when added) — see `feat/routing-tabs` change |
| Avatar | `src/components/Avatar.tsx` (custom, takes initials + image URL) |
| Empty state | `src/components/EmptyState.tsx` (icon + title + body + CTA) |

## 9. Motion principles

- **Reanimated 4 + Worklets.** All animations run on the UI thread. Never use
  the legacy `Animated` API.
- **Durations:** `120ms` (press feedback), `220ms` (transitions), `320ms` (sheet
  open/close), `420ms` (hero entrance).
- **Easings:** `cubic-bezier(0.2, 0, 0, 1)` (default), `cubic-bezier(0.4, 0, 0.2, 1)`
  (material standard).
- **Reduced motion:** gate every animation with `useReducedMotion()` and short-
  circuit to a 0ms duration when `prefers-reduced-motion: reduce` is set.
- **Stagger:** 30ms between items, capped at 6 items, in lists.

## 10. Accessibility

- All interactive components must have an `accessibilityLabel` derived from
  visible text, never duplicated.
- Color contrast ≥ 4.5:1 for body, ≥ 3:1 for large text. Token values above meet
  WCAG AA in their respective modes.
- Tap targets ≥ 44 × 44 on iOS, ≥ 48 × 48 on Android.
- Respect system font scale; never lock text size.
- VoiceOver / TalkBack labels must be localized.

## 11. Localization

- All user-facing strings go through `i18n` (to be added under `src/i18n/` in a
  later change). No hard-coded strings in components.
- Date, time, and number formatting MUST go through `Intl.*` via the i18n layer.
- Default locale: `en`. Spanish (`es`) is the next priority.

## 12. What this doc does NOT cover yet

- Empty / loading / error visual states for screens we have not designed.
- Brand wordmark, logo system, motion identity (deferred to `feat/brand-system`).
- Marketing site styling (separate doc, separate repo).

When a new pattern emerges, propose it as an OpenSpec change
(`openspec/changes/feat/design-<topic>/`) before committing it here.