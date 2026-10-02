# Contributing — Card Taxi

This project uses **GitHub Flow**: `main` is always deployable, every change ships through a pull request.

## TL;DR

```bash
# 1. Sync main
git checkout main
git pull --rebase origin main

# 2. Branch off main with a Conventional Commits prefix
git checkout -b feat/<scope>-<short-name>
# examples:
#   feat/map-add-taxi-marker
#   fix/auth-token-refresh
#   chore/bump-expo-57
#   docs/update-readme

# 3. Build, lint, test
bun run lint
bunx tsc --noEmit
bun run start    # smoke test on at least one target

# 4. Commit (Conventional Commits)
git commit -m "feat(map): add taxi marker with smooth pin animation"

# 5. Push and open a PR targeting main
git push -u origin HEAD
gh pr create --base main --fill --reviewer PandaDesigner
```

## Why GitHub Flow

- `main` is the single source of truth and must always be in a deployable state.
- Branches are short-lived (hours, not days).
- Every change is reviewed via PR before merging.
- Merge to `main` **is** the deploy — keep history linear via squash.

## Branch protection (already enforced)

- PR required to merge into `main`
- **Linear history required** — only squash or rebase merges (no merge commits)
- No force-push to `main`, no branch deletion
- Solo maintainer? `required_approving_review_count` is `0` so you can self-merge. Increase to `1` once a second reviewer joins.

## Conventions

| Thing | Convention |
| --- | --- |
| Commit format | [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `perf:`, `test:`) |
| Branch prefix | `<type>/<scope>-<short-name>` (matches commit type) |
| PR template | `.github/PULL_REQUEST_TEMPLATE.md` (auto-loaded) |
| Default branch | `main` |
| Code style | Expo / TypeScript defaults; `expo lint` must be clean |
| Commits per PR | Small, single-purpose. Split unrelated changes into separate PRs |

## PR rules

1. **One PR = one purpose.** Don't bundle a refactor with a feature.
2. **Rebase before requesting review.** `git fetch origin && git rebase origin/main` then `--force-with-lease` push.
3. **Fill the template.** Screenshots for UI changes, verification steps, rollback plan.
4. **Self-review your diff** in the GitHub UI before pinging reviewers.
5. **Address every comment** — resolve threads or push back with a reason.
6. **Squash merge.** The squash commit becomes the PR title; write it like a real commit (`feat(map): …`).
7. **Delete the source branch** automatically on merge (already configured).

## Local pre-merge checklist

- [ ] `git status` is clean
- [ ] `bun run lint` passes
- [ ] `bunx tsc --noEmit` passes
- [ ] Smoke-tested on at least one target (iOS sim, Android emulator, or `expo start --web`)
- [ ] No `console.log`, `debugger`, or commented-out code left behind
- [ ] No `.env*`, `*.pem`, or other secrets staged

## After merge

1. Delete the local branch: `git branch -d <name>`
2. Pull the new `main`: `git pull --rebase origin main`
3. If you stashed anything: `git stash drop` after confirming it's gone

## Releasing

We use Expo's standard release pipeline (EAS Build / Submit / Update — see the `eas-*` skills when ready). A merge to `main` triggers the next OTA update; a tagged commit triggers a store build.