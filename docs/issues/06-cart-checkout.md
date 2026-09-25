---
title: "Cart & checkout"
labels: [backend, frontend]
---

## Skills you'll practice
Stateful API design, client-side cart state, the mechanics of a checkout flow (this is the issue with the most "real world" surface area — stock, totals, race conditions).

## Description
**Backend** (`apps/backend/src/routes/cart.js`):
- `GET /cart` — current user's cart items + a computed total
- `POST /cart` — add a product (or increment quantity if already in cart)
- `PATCH /cart/:productId` — update quantity
- `DELETE /cart/:productId` — remove an item
- `POST /checkout` — validates stock is still available for every item, creates an `Order` + `OrderItem`s, clears the cart, returns the order. **v1: no real payment** — just mark the order `PAID` directly. Stretch goal below covers Stripe.

**Frontend:**
- A `CartContext` mirroring the backend cart, with optimistic updates (update the UI immediately, roll back if the API call fails)
- A cart page/drawer showing items, quantities, running total
- A checkout page that calls `POST /checkout` and shows an order confirmation

## Acceptance criteria
- [ ] Adding the same product twice increments quantity rather than creating a duplicate row
- [ ] Cart total on the frontend matches what the backend computes (compute it server-side, don't trust a client-sent total)
- [ ] Checking out with more quantity than available stock fails with a clear error, doesn't create a broken order
- [ ] Checkout succeeds, order appears in the database with correct `OrderItem` snapshots (see the price-snapshot note in `docs/issues/01-database-schema.md`)
- [ ] Cart clears after a successful checkout

## Stretch goal: real Stripe test-mode integration
Once the mock flow above works end to end, swap the "mark as paid directly" step for Stripe's test mode (free, no real money, no real bank account needed): create a Checkout Session server-side, redirect the user to Stripe's hosted checkout page, handle the webhook that confirms payment. This is genuinely worth doing if there's time — it's the part of this project closest to what a real e-commerce job looks like.

## Resources
- [Stripe — Accept a payment (Checkout)](https://stripe.com/docs/checkout/quickstart) (for the stretch goal)
- Search "optimistic UI updates react" for the cart-state pattern
- On race conditions: think about what happens if two checkout requests for the last unit of a product land at nearly the same time — doesn't need a perfect solution for v1, but worth writing a comment acknowledging it

## Notes
Depends on `docs/issues/01-database-schema.md`, `docs/issues/02-auth-api.md` (cart is per-user), and `docs/issues/04-catalog-api.md` (needs stock data). This is the most complex issue in the list — good one to split into two PRs (cart, then checkout) rather than one large one.
