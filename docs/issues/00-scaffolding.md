---
title: "Project scaffolding & tooling"
labels: [devops, good-first-issue]
---

## Skills you'll practice
Repo/tooling setup, npm, ESLint/Prettier config, Docker basics, GitHub Actions basics.

## Why this issue exists
Everything else in this repo assumes `npm install && npm run dev` just works in both `apps/backend` and `apps/frontend`. Right now it doesn't — this issue turns the README's instructions into reality, so the next nine issues aren't all blocked on figuring out setup themselves.

## Description
Get both apps from "scaffold" to "actually runs":

- `apps/backend`: run `npm init`, install Express + Prisma + the auth libraries listed in `apps/backend/README.md`, get a minimal `src/index.js` responding on `GET /health` with `{ status: "ok" }`
- `apps/frontend`: generate the real Vite + React scaffold per `apps/frontend/README.md`, wire up Tailwind, get the default page rendering
- Add ESLint + Prettier configs to both apps (shared config at the repo root is fine)
- Add a minimal GitHub Actions workflow (`.github/workflows/ci.yml`) that runs lint on every PR — tests can come later once `docs/issues/08-testing-ci.md` lands
- Confirm `docker compose up -d` + `npx prisma migrate dev` actually creates the `User` table from the starter `schema.prisma`

## Acceptance criteria
- [ ] `cd apps/backend && npm install && npm run dev` starts a server, `curl localhost:4000/health` returns `200`
- [ ] `cd apps/frontend && npm install && npm run dev` serves the default Vite+React page with Tailwind classes visibly working
- [ ] `docker compose up -d` starts Postgres cleanly; `npx prisma migrate dev` applies without errors
- [ ] ESLint runs clean (`npm run lint`) in both apps
- [ ] CI workflow runs on a test PR and shows green

## Resources
- [Vite docs — Getting Started](https://vitejs.dev/guide/)
- [Express — Getting Started](https://expressjs.com/en/starter/installing.html)
- [Prisma — Quickstart](https://www.prisma.io/docs/getting-started/quickstart)
- [GitHub Actions — Node.js quickstart](https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs)

## Notes
This issue blocks almost everything else — good one to pick up first, and a good one to pair on even if you're confident, since the decisions made here (folder conventions, lint rules) affect every later PR.
