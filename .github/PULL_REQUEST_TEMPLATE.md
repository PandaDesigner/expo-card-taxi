## Summary

<!-- One or two sentences: what changed and why. -->

## Type of change

- [ ] `feat` — new user-facing capability
- [ ] `fix` — bug fix
- [ ] `refactor` — no behavior change
- [ ] `chore` — tooling, deps, config, docs
- [ ] `docs` — documentation only
- [ ] `perf` — performance improvement
- [ ] `test` — tests only

## Linked issue

<!-- `Closes #123` or `Refs #123` — leave blank if none. -->

## Changes

<!-- Bulleted list of the meaningful changes. Skip noise (lockfile churn, generated files). -->

-

## Screenshots / Recordings

<!-- Required for any UI change. Native + Web parity shots if both targets move. -->

## Verification

<!-- What you executed locally to prove the change works. -->

- [ ] `bun run lint` (or `npm run lint`)
- [ ] `bun run start` smoke test on iOS / Android / Web
- [ ] TypeScript: `bunx tsc --noEmit`
- [ ] Manual test of the affected flow

## Risk & rollback

<!-- What can break? How do we revert (revert commit, disable flag, delete branch)? -->

## Checklist

- [ ] Branch is rebased on `main` (`git fetch origin && git rebase origin/main`)
- [ ] Commits use Conventional Commits (`feat:`, `fix:`, `chore:` …)
- [ ] No commits authored by AI agents that weren't reviewed
- [ ] No secrets, `.env*` files, or build artifacts included
- [ ] Public API / schema changes are called out above