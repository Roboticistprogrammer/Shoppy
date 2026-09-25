---
title: "Database schema — products, cart, orders"
labels: [database, backend]
---

## Skills you'll practice
Relational data modeling, foreign keys and relations, Prisma schema syntax, migrations.

## Why this issue exists
Almost every other backend issue needs tables that don't exist yet. This issue designs and migrates them, so `docs/issues/04-catalog-api.md` and later ones have something real to query.

## Description
Extend `apps/backend/prisma/schema.prisma` (which currently only has `User`) with:

- `Category` — `id`, `name`, `slug`
- `Product` — `id`, `name`, `description`, `priceCents` (store money as integer cents, not float), `imageUrl`, `stock`, relation to `Category`
- `CartItem` — relation to `User` and `Product`, `quantity`
- `Order` — relation to `User`, `status` (enum: `PENDING`, `PAID`, `SHIPPED`, `CANCELLED`), `totalCents`, `createdAt`
- `OrderItem` — relation to `Order` and `Product`, `quantity`, `priceCentsAtPurchase` (snapshot the price — don't just reference `Product.priceCents`, since prices change later)

Also write a seed script (`prisma/seed.js` or `.ts`) that inserts a handful of categories and ~15 products, so everyone else has real data to build against instead of an empty database.

## Acceptance criteria
- [ ] Schema models above exist with correct relations (check both directions — e.g. `User.orders` and `Order.user`)
- [ ] `npx prisma migrate dev --name add-catalog-and-orders` runs clean
- [ ] `npx prisma studio` shows all tables with correct columns
- [ ] Seed script populates categories + products; documented in `apps/backend/README.md` how to run it (`npx prisma db seed` or similar)
- [ ] A short comment in the schema file explaining the `priceCentsAtPurchase` snapshot decision (why not just join to `Product`)

## Resources
- [Prisma — Data model](https://www.prisma.io/docs/orm/prisma-schema/data-model/models)
- [Prisma — Relations](https://www.prisma.io/docs/orm/prisma-schema/data-model/relations)
- [Prisma — Seeding](https://www.prisma.io/docs/orm/prisma-migrate/workflows/seeding)
- Why store money as integer cents: search "never use float for currency" — short, worth reading once, applies everywhere

## Notes
Depends on `docs/issues/00-scaffolding.md` being done first (needs a running Postgres + Prisma setup). Blocks nearly everything else — worth prioritizing.
