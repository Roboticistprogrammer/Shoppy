---
title: "Order history & admin panel"
labels: [backend, frontend]
---

## Skills you'll practice
CRUD design, role-based access control, building an internal/admin-style UI (different priorities than a customer-facing one: density over polish).

## Description
**Backend:**
- `GET /orders` — current user's own order history
- `GET /admin/orders` — all orders, admin-only
- `POST /admin/products`, `PATCH /admin/products/:id`, `DELETE /admin/products/:id` — product management, admin-only
- Middleware that checks `req.user.role === 'ADMIN'` and returns `403` otherwise — apply it to every `/admin/*` route

**Frontend:**
- `/orders` page — logged-in user's past orders with status and items
- `/admin` section (only reachable/visible to admin users) — a table of all orders, and a simple form to add/edit/delete products

## Acceptance criteria
- [ ] A non-admin user hitting any `/admin/*` endpoint directly (e.g. via curl) gets `403`, regardless of what the frontend hides
- [ ] Order history shows only the logged-in user's own orders, never anyone else's
- [ ] Admin can add a new product and it immediately appears in the public catalog
- [ ] Admin can edit stock/price and see it reflected on the product detail page
- [ ] Deleting a product that has existing orders doesn't break order history (consider soft-delete, or just block deletion if orders reference it — document whichever you pick)

## Resources
- [Role-based access control — a short primer](https://www.osohq.com/post/role-based-access-control-rbac) (any similar overview is fine)
- Prisma docs on `include`/relations for pulling order + order-items together

## Notes
Depends on `docs/issues/02-auth-api.md` (for role checking) and `docs/issues/06-cart-checkout.md` (orders need to exist first). The `403`-even-if-frontend-hides-it acceptance criterion is the important one here — it's a common real-world bug (relying on the UI to hide something instead of enforcing it server-side).
