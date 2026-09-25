---
title: "Catalog API — list, search, filter products"
labels: [backend]
---

## Skills you'll practice
REST endpoint design, query parameters, pagination, database queries with Prisma.

## Description
Build in `apps/backend/src/routes/products.js`:

- `GET /products` — supports `?category=`, `?search=` (matches name/description), `?page=` and `?limit=` for pagination, returns products + total count
- `GET /products/:id` — single product detail, `404` if it doesn't exist
- `GET /categories` — list all categories (for building filter UI)

Keep pagination genuinely working — don't fetch everything and slice in JS; use Prisma's `skip`/`take` so it scales the way a real API would need to.

## Acceptance criteria
- [ ] `GET /products?page=2&limit=10` returns the correct slice and a `total` count for building pagination UI
- [ ] `GET /products?search=shirt` matches case-insensitively against name and description
- [ ] `GET /products?category=electronics` filters correctly
- [ ] `GET /products/:id` for a nonexistent id returns `404` with a clear error body, not a raw stack trace
- [ ] Response shapes are documented (a short comment block or a `docs/api.md` entry) so the frontend issue doesn't have to guess

## Resources
- [Prisma — Pagination](https://www.prisma.io/docs/orm/prisma-client/queries/pagination)
- [Prisma — Filtering and sorting](https://www.prisma.io/docs/orm/prisma-client/queries/filtering-and-sorting)
- [REST API design — pagination patterns](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Filtering-Sorting-and-Pagination/) (any similar overview works too)

## Notes
Depends on `docs/issues/01-database-schema.md` and its seed data. Blocks `docs/issues/05-catalog-frontend.md`.
