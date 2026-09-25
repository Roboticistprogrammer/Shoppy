# Shoppy — a learning e-commerce platform

Scope is deliberately small. This is not meant to become a real store — it's meant to touch auth, a real database, a REST API, and a frontend that talks to it, without sprawling into features nobody needs to practice.

## What we're building

A minimal but complete e-commerce flow:

- Browse products, search and filter by category
- User accounts (register / log in / log out)
- A cart that persists per user
- Checkout (mock payment for v1; real Stripe test-mode integration is a stretch goal)
- Order history for the logged-in user
- A small admin panel to add/edit products and view orders

That's it. No recommendations engine, no reviews, no wishlist — those are fine as stretch issues once the core loop works.

## Tech stack

| Layer | Choice | Why |
|---|---|---|
| Frontend | React + Vite + Tailwind CSS | Fastest path from zero to a working UI; huge amount of learning material |
| Backend | Node.js + Express (REST API) | Same language as the frontend — one less context switch for beginners |
| Database | PostgreSQL + Prisma ORM | Prisma's schema file doubles as living documentation of the data model |
| Auth | JWT (access + refresh tokens), bcrypt for password hashing | The standard pattern you'll see in almost every real-world API |
| Payments | Mock checkout for v1 → Stripe test mode as a stretch goal | Stripe test mode is free and a genuinely useful thing to learn, but not a v1 blocker |
| Local dev | Docker Compose (Postgres only) | Nobody has to install Postgres by hand |
| Deployment (stretch) | Render / Railway / Fly.io | Free tiers, simple enough to deploy from a Dockerfile |

If your team already knows a different stack better, swap it — the workstream breakdown below still applies. The one thing worth keeping is "frontend and backend in the same language," since it halves the ramp-up for anyone newer to web dev.

## Architecture

```
┌─────────────┐       REST / JSON        ┌──────────────┐       SQL       ┌────────────┐
│   React     │ ───────────────────────▶ │   Express    │ ──────────────▶ │ PostgreSQL │
│  (Vite app) │ ◀─────────────────────── │   REST API   │ ◀────────────── │  (Prisma)  │
└─────────────┘                          └──────────────┘                 └────────────┘
                                                 │
                                                 ▼
                                          ┌──────────────┐
                                          │ Stripe (test │
                                          │ mode, stretch│
                                          └──────────────┘
```

The frontend never talks to the database directly — everything goes through the API. That boundary is worth keeping strict even though it's a small project; it's the same boundary Aerobench's `app` service keeps from everything NVIDIA-side.

## Repo structure

```
Shoppy/
├── apps/
│   ├── backend/          # Express API
│   │   ├── src/
│   │   ├── prisma/
│   │   │   └── schema.prisma
│   │   ├── .env.example
│   │   └── README.md     # backend-specific setup
│   └── frontend/         # React + Vite app
│       └── README.md     # frontend-specific setup
├── docs/
│   └── issues/           # one file per issue — copy each into a GitHub issue
├── docker-compose.yml    # local Postgres
├── .env.example
├── CONTRIBUTING.md
└── README.md             # this file
```

## Getting started

**Prerequisites:** Node.js 20+, Docker Desktop (or any Docker engine), Git.

```bash
# 1. Clone and enter the repo
git clone <your-repo-url> teamcart && cd teamcart

# 2. Start Postgres locally
docker compose up -d

# 3. Set up the backend
cd apps/backend
cp .env.example .env          # fill in DATABASE_URL / JWT_SECRET
npm install
npx prisma migrate dev        # creates tables from schema.prisma
npm run dev                   # API on http://localhost:4000

# 4. In a second terminal, set up the frontend
cd apps/frontend
npm install
npm run dev                   # app on http://localhost:5173
```

Each `apps/*/README.md` has the fuller setup notes for that half of the stack — read those before opening your issue.

## Learning modules / workstreams

Each row is roughly one issue. Assign by current strength, not by who "should" learn it — pair the person newer to the topic with whoever's more confident in it, working the same issue together rather than in isolation.

| Workstream | Skills practiced | Issue |
|---|---|---|
| Project scaffolding & tooling | Monorepo setup, linting, Docker, CI basics | `docs/issues/00-scaffolding.md` |
| Database schema | Relational modeling, Prisma, migrations | `docs/issues/01-database-schema.md` |
| Auth API | JWT, password hashing, middleware | `docs/issues/02-auth-api.md` |
| Auth frontend | Forms, client-side auth state, protected routes | `docs/issues/03-auth-frontend.md` |
| Catalog API | REST design, pagination, search/filter queries | `docs/issues/04-catalog-api.md` |
| Catalog frontend | Data fetching, component design, loading/error states | `docs/issues/05-catalog-frontend.md` |
| Cart & checkout | Client state, API design for a stateful flow | `docs/issues/06-cart-checkout.md` |
| Orders & admin panel | CRUD, role-based access | `docs/issues/07-orders-admin.md` |
| Testing & CI | Unit/integration tests, GitHub Actions | `docs/issues/08-testing-ci.md` |
| Deployment | Dockerfiles, environment config, hosting | `docs/issues/09-deployment.md` |

The [full-stack roadmap article](https://dev.to/developerhint/full-stack-web-developer-roadmap-2026-complete-guide-from-beginner-to-advanced-fam) is a good map of where each workstream sits in the bigger picture, if anyone wants to see how their one issue connects to everything else.

## Suggested milestones

- **M0 — Setup:** scaffolding issue done, everyone's dev environment runs
- **M1 — Foundations:** database schema + auth (API and frontend) merged
- **M2 — Core loop:** catalog (API and frontend) merged, products are browsable
- **M3 — Transactions:** cart, checkout, and orders merged — a user can complete a full purchase
- **M4 — Polish:** admin panel, tests, CI green
- **M5 — Ship it:** deployed somewhere with a real URL, even a free-tier one

## How we work

See `CONTRIBUTING.md` for branch naming, commit style, and the PR checklist. Short version: one issue → one branch → one PR that links back to the issue → one teammate reviews it before merge.

## License

MIT — see `LICENSE`. This is a learning project; do whatever's useful with it.
