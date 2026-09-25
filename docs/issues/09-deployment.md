---
title: "Deployment"
labels: [devops]
---

## Skills you'll practice
Dockerizing an app, environment configuration for production vs. local, deploying to a real host.

## Description
- Write a `Dockerfile` for `apps/backend` (multi-stage: install deps, build if using TypeScript, run)
- Write a `Dockerfile` for `apps/frontend` (build the static Vite output, serve it — nginx or a simple static server)
- Pick a free-tier host — Render, Railway, and Fly.io all work and all have straightforward "deploy from a Dockerfile" paths — and get both services live
- Set up a managed Postgres instance on whichever platform you choose (most free tiers include one) and point the deployed backend's `DATABASE_URL` at it
- Document the live URLs and the deploy process in `docs/DEPLOYMENT.md`

## Acceptance criteria
- [ ] Backend is reachable at a public URL, `/health` returns `200`
- [ ] Frontend is reachable at a public URL and successfully talks to the deployed backend (not `localhost`)
- [ ] Production `DATABASE_URL` and JWT secrets are set via the host's environment variable settings, never committed to the repo
- [ ] `docs/DEPLOYMENT.md` has enough detail that someone else on the team could redeploy from scratch
- [ ] CORS is configured on the backend to allow the deployed frontend's origin (and rejects others)

## Resources
- [Render — Deploy a Docker web service](https://render.com/docs/deploy-a-docker-app)
- [Railway — docs](https://docs.railway.app/)
- [Fly.io — docs](https://fly.io/docs/)

## Notes
This is the last issue on purpose — deploying something half-built teaches less than deploying something that actually works end to end. Good one to save for after M3/M4 in the README's milestones, ideally right before the team wants to show the finished thing to anyone outside the team.
