---
title: "Testing & CI"
labels: [devops, backend, frontend]
---

## Skills you'll practice
Unit and integration testing, mocking, GitHub Actions.

## Why this issue exists
Nothing in this repo has automated tests yet — everything's been verified by hand via the acceptance-criteria checklists. That's fine for learning speed early on, but this issue is what turns "I tested it locally" into something the whole team can trust on every PR.

## Description
- **Backend:** set up Vitest or Jest. Write integration tests for the auth endpoints (register, login, protected route with/without a valid token) and the cart/checkout flow (using a test database, not the dev one — see resources)
- **Frontend:** set up Vitest + React Testing Library. Write component tests for at least the auth forms and the product grid's loading/error states
- **CI:** extend `.github/workflows/ci.yml` (created in `docs/issues/00-scaffolding.md`) to run both test suites on every PR, not just lint

## Acceptance criteria
- [ ] `npm test` in `apps/backend` runs and passes, covering at least auth + checkout
- [ ] `npm test` in `apps/frontend` runs and passes, covering at least the forms
- [ ] Tests use a separate test database (or mocked Prisma client) — never the real dev data
- [ ] CI runs both suites on every PR and blocks merge on failure
- [ ] A short `docs/TESTING.md` note on how to run tests locally and add a new one

## Resources
- [Vitest docs](https://vitest.dev/)
- [React Testing Library — docs](https://testing-library.com/docs/react-testing-library/intro/)
- [Prisma — testing with a separate database](https://www.prisma.io/docs/orm/prisma-client/testing/integration-testing)

## Notes
This issue works best once most of the core features (auth, catalog, cart, checkout) already exist — testing something that doesn't exist yet is backwards. A reasonable point to pick this up is once M3 in the README's milestones is done.
