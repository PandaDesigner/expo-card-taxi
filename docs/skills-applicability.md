# Skills Applicability — Card Taxi

> Maps **task types** to the **`SKILL.md`** files that MUST be loaded **before**
> starting work. This is the index, not the contract — always load the full
> `SKILL.md` content via `read`, do not summarise from this table.
>
> Auto-generated registry: [`../.atl/skill-registry.md`](../.atl/skill-registry.md)
> (regenerate with `/skill-registry:refresh`).

## How to use this

1. Identify the row that best matches what you are about to do.
2. Read every `SKILL.md` path listed in the "Skills to load" column **before**
   touching code.
3. If the change is delegated to a subagent, pass the full paths in the task
   prompt so the subagent loads them in its own context.
4. If a task spans multiple rows, load the union of all skills.

## Task → skills matrix

| Task type | Skills to load (full path) |
| --- | --- |
| **Spec-driven change (any)** | `~/.config/opencode/skills/sdd-explore/SKILL.md`, `~/.config/opencode/skills/sdd-propose/SKILL.md`, `~/.config/opencode/skills/sdd-spec/SKILL.md`, `~/.config/opencode/skills/sdd-design/SKILL.md`, `~/.config/opencode/skills/sdd-tasks/SKILL.md`, `~/.config/opencode/skills/sdd-apply/SKILL.md`, `~/.config/opencode/skills/sdd-verify/SKILL.md`, `~/.config/opencode/skills/sdd-archive/SKILL.md` |
| **Initialize / re-bootstrap OpenSpec** | `~/.config/opencode/skills/sdd-init/SKILL.md`, `~/.config/opencode/skills/sdd-onboard/SKILL.md` |
| **Routing (Expo Router)** | `~/.pi/agent/skills/expo-router/SKILL.md`, `~/.pi/agent/skills/expo-project-structure/SKILL.md` |
| **Native UI components** | `~/.pi/agent/skills/expo-ui/SKILL.md`, `~/.pi/agent/skills/expo-native-ui/SKILL.md`, `~/.agents/skills/building-native-ui/SKILL.md` |
| **Expo Modules API (Swift/Kotlin)** | `~/.pi/agent/skills/expo-module/SKILL.md` (new module) or `~/.pi/agent/skills/expo-migrate-module/SKILL.md` (1.0 → 2.0) |
| **Native iOS App Clip** | `~/.pi/agent/skills/expo-app-clip/SKILL.md` |
| **Brownfield (existing native app)** | `~/.pi/agent/skills/expo-brownfield/SKILL.md` |
| **Animations (Reanimated 4 / GSAP)** | `~/.agents/skills/vercel-react-native-skills/SKILL.md`, `~/.agents/skills/gsap-core/SKILL.md` (only if GSAP is added) |
| **API / data fetching** | `~/.pi/agent/skills/expo-data-fetching/SKILL.md`, `~/.agents/skills/native-data-fetching/SKILL.md`, `~/.agents/skills/ai-sdk-5/SKILL.md` (only if using Vercel AI SDK) |
| **Web migration / DOM component** | `~/.pi/agent/skills/expo-dom/SKILL.md`, `~/.pi/agent/skills/expo-web-to-native/SKILL.md` |
| **Upgrade Expo SDK** | `~/.pi/agent/skills/expo-upgrade/SKILL.md`, `~/.agents/skills/upgrading-expo/SKILL.md` |
| **Styling (Tailwind / NativeWind / Uniwind)** | `~/.pi/agent/skills/expo-tailwind-setup/SKILL.md`, `~/.agents/skills/tailwind-4/SKILL.md`, `~/.agents/skills/migrate-nativewind-to-uniwind/SKILL.md` |
| **Build, ship to stores (EAS)** | `~/.pi/agent/skills/eas-app-stores/SKILL.md`, `~/.agents/skills/expo-app-stores/SKILL.md` |
| **EAS Hosting / API routes** | `~/.pi/agent/skills/eas-hosting/SKILL.md`, `~/.agents/skills/expo-api-routes/SKILL.md` |
| **EAS Update (OTA)** | `~/.pi/agent/skills/eas-update-insights/SKILL.md` |
| **EAS Workflows (CI/CD)** | `~/.pi/agent/skills/eas-workflows/SKILL.md`, `~/.agents/skills/expo-cicd-workflows/SKILL.md` |
| **EAS Observe (metrics)** | `~/.pi/agent/skills/eas-observe/SKILL.md` |
| **EAS Simulator (cloud device)** | `~/.pi/agent/skills/eas-simulator/SKILL.md` |
| **Dev client build & distribution** | `~/.pi/agent/skills/expo-dev-client/SKILL.md`, `~/.agents/skills/expo-deployment/SKILL.md` |
| **Testing** | `~/.agents/skills/playwright/SKILL.md` (web E2E), `~/.agents/skills/setup-react-native-storybook/SKILL.md` (Storybook) |
| **TypeScript quality** | `~/.agents/skills/typescript/SKILL.md`, `~/.agents/skills/typescript-best-practices/SKILL.md`, `~/.agents/skills/typescript-pro/SKILL.md` |
| **State management** | `~/.agents/skills/zustand-5/SKILL.md`, `~/.agents/skills/react-19/SKILL.md` |
| **Validation (forms / API)** | `~/.agents/skills/zod-4/SKILL.md` |
| **Design audit / polish** | `~/.agents/skills/impeccable/SKILL.md`, `~/.agents/skills/web-design-guidelines/SKILL.md` |
| **Architecture diagram (for design.md)** | `~/.pi/agent/skills/archify/SKILL.md` |
| **Code review / PR feedback** | `~/.pi/agent/skills/archify-review/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/comment-writer/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/branch-pr/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/chained-pr/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/work-unit-commits/SKILL.md` |
| **Triage / decide an issue** | `~/.pi/agent/npm/node_modules/gentle-pi/skills/issue-creation/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/judgment-day/SKILL.md` |
| **Write / update a doc / README / RFC** | `~/.pi/agent/npm/node_modules/gentle-pi/skills/cognitive-doc-design/SKILL.md` |
| **Commit planning** | `~/.pi/agent/npm/node_modules/gentle-pi/skills/work-unit-commits/SKILL.md` |
| **Spec-driven / skill creation** | `~/.pi/agent/npm/node_modules/gentle-pi/skills/skill-creator/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/skill-improver/SKILL.md`, `~/.pi/agent/npm/node_modules/gentle-pi/skills/skill-registry/SKILL.md` |
| **Marketing / landing / SEO** | `~/.pi/agent/skills/market-suite/SKILL.md` (routes to the right sub-skill) |
| **Architecture / OOP review** | `~/.agents/skills/oop-architecture-review/SKILL.md`, `~/.agents/skills/patrones/SKILL.md`, `~/.agents/skills/vercel-composition-patterns/SKILL.md`, `~/.agents/skills/vercel-react-best-practices/SKILL.md` |
| **Web scraping / browser automation** | `~/.agents/skills/agent-browser/SKILL.md` |
| **Image generation (assets)** | `~/.agents/skills/ai-image-generation/SKILL.md`, `~/.agents/skills/imagegen-frontend-mobile/SKILL.md`, `~/.agents/skills/imagegen-frontend-web/SKILL.md`, `~/.agents/skills/brandkit/SKILL.md`, `~/.agents/skills/nano-banana-2/SKILL.md`, `~/.agents/skills/gpt-image/SKILL.md` |
| **Video generation (assets)** | `~/.agents/skills/image-to-video/SKILL.md` |
| **3D / print assets** | `~/.agents/skills/meshy-3d-agent/SKILL.md`, `~/.agents/skills/meshy-3d-generation/SKILL.md`, `~/.agents/skills/meshy-3d-printing/SKILL.md` |
| **InsForge backend (DB / auth / storage)** | `~/.agents/skills/insforge/SKILL.md`, `~/.agents/skills/insforge-cli/SKILL.md`, `~/.agents/skills/insforge-debug/SKILL.md`, `~/.agents/skills/insforge-integrations/SKILL.md` |
| **Agent UI component (React)** | `~/.agents/skills/agent-ui/SKILL.md` |
| **Add auth (Better Auth)** | `~/.agents/skills/create-auth-skill/SKILL.md` |
| **Search docs / libraries** | `~/.agents/skills/context7/SKILL.md`, `~/.agents/skills/context7-mcp/SKILL.md` |
| **WordPress project** | `~/.agents/skills/wordpress-pro/SKILL.md` |
| **Django REST** | `~/.agents/skills/django-drf/SKILL.md` |
| **Next.js** | `~/.agents/skills/nextjs-15/SKILL.md`, `~/.agents/skills/nextjs-app-router-fundamentals/SKILL.md` |
| **Pytest** | `~/.agents/skills/pytest/SKILL.md` |
| **Go testing / Bubbletea** | `~/.agents/skills/go-testing/SKILL.md` |
| **Storybook (RN)** | `~/.agents/skills/setup-react-native-storybook/SKILL.md` |
| **Tailwind (web)** | `~/.agents/skills/tailwind-4/SKILL.md` |
| **HTTP / Zod-validated client** | `~/.agents/skills/http-session-consumer/SKILL.md` |
| **Expo skill feedback** | `~/.pi/agent/skills/expo-skill-feedback/SKILL.md` |
| **Expo skill scaffolding (cross-repo)** | `~/.pi/agent/skills/expo-skill-eval/SKILL.md` |
| **MCP / docs lookup** | `mcp` tool or its namespaced proxies (`mcp__context7`, `mcp__docs`, `mcp__agents`) |
| **Background / Fusion tasks** | `pi-background-tasks` system (use `bg_run`, `bg_delegate`, `fusion_*`) |
| **Named subagent delegation** | `pi-subagents` system (use `subagent` tool) |

## Universal load (any task)

These three are loaded on every change, regardless of type. They encode the
project's GitHub Flow + OpenSpec discipline and the agent's overall posture.

- [`AGENTS.md`](../../AGENTS.md) — read this directly; do not rely on this table.
- [`openspec/AGENTS.md`](../../openspec/AGENTS.md) — OpenSpec workflow.
- [`DESIGN.md`](../../DESIGN.md) — tokens and component policy.

## Tasks that should NOT load a skill

If the task fits any of these, skip the skill lookup entirely:

- Reading or summarising existing code with no planned mutation.
- Updating `.atl/skill-registry.md` (the registry itself is the contract).
- A typo / one-line comment fix.
- Renaming a symbol with no behaviour change (run `grep` to confirm).

## Maintaining this file

When a new `SKILL.md` shows up in `.atl/skill-registry.md` that fits a recurring
task type in this project, add a row. Keep the rule:

> One row per **task type**, not per skill. A row can list multiple skills.

Do not duplicate a row just because two skills are listed together in another doc;
merge them if the task types overlap.