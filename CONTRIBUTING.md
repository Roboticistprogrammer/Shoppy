# Contributing

This is a small team learning together, so the process is lighter than a real production repo — but keeping even a light version of it is the point. Real teams work this way; practicing it here is part of what you're learning.

## Workflow

1. **Pick up an issue.** Each issue in `docs/issues/` gets opened as a real GitHub Issue and assigned to one person (or a pair — see below). Don't start work without an issue; if you're doing something not covered by one, open a new issue first, even a short one.
2. **Branch from `main`:**
   ```
   git checkout -b feature/<issue-number>-<short-description>
   # e.g. feature/02-auth-api
   ```
3. **Commit as you go**, using [Conventional Commits](https://www.conventionalcommits.org/):
   - `feat: add JWT refresh endpoint`
   - `fix: correct cart total calculation`
   - `docs: update backend setup steps`
   - `chore: add eslint config`
   - `test: add tests for product search`
4. **Open a PR early**, even in draft. Link it to the issue (`Closes #12`) so it auto-closes on merge. A PR open on day one, updated as you go, is easier for a teammate to follow than one dropped in finished on day five.
5. **Get one review before merging.** Pair with whoever's more confident in that workstream if that's not already how you got there. The point of review here isn't gatekeeping — it's a second person understanding what got built, since everyone needs to be able to work across this codebase later.
6. **Keep PRs small.** If an issue is turning into a 900-line diff, that's a sign to split it — open a follow-up issue for the rest rather than trying to land everything at once.

## Pairing, not isolating

If you're newer to a workstream's core skill (say, JWT auth, or SQL joins), don't take that issue solo and struggle silently. Pair with whoever's stronger there — same issue, same branch, working through it together. You'll ship faster and actually retain the pattern, versus watching a tutorial in isolation and separately trying to apply it under deadline pressure.

## Code style

- **Formatting:** Prettier (config in the repo root — run `npm run format` before committing)
- **Linting:** ESLint — `npm run lint` in each app; fix warnings before opening a PR, don't just silence them
- **Naming:** camelCase for variables/functions, PascalCase for React components, kebab-case for file names outside of components

## Issue labels

Use these when opening issues in GitHub, so the board stays legible:

- `backend` / `frontend` / `database` / `auth` / `devops` — which workstream
- `good-first-issue` — safe for whoever's least confident that week
- `stretch` — not required for the core loop (Stripe integration, wishlist, etc.)
- `blocked` — waiting on another issue; note which one in the issue body

## Weekly check-in

Once a week, everyone shows what runs — even if it's broken or half-built. Two minutes each, no slides. This matters more than a status report: seeing something on screen surfaces integration problems (two people's API shapes not matching, say) far earlier than a verbal update would.

## Environment variables

Never commit a real `.env` file. `.env.example` in each app lists what's needed with placeholder values — copy it to `.env` locally and fill in your own.
