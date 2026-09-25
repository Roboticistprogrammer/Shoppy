---
title: "Auth API — register, login, JWT"
labels: [backend, auth]
---

## Skills you'll practice
Password hashing, JWT issuing/verification, Express middleware, protected routes.

## Why this issue exists
This is the workstream most directly tied to what the team flagged as a skill gap. It's also foundational — cart, checkout, and orders all need to know who's making the request.

## Description
Build these endpoints in `apps/backend/src/routes/auth.js`:

- `POST /auth/register` — email + password + name → hash the password with bcrypt, create a `User`, return an access token
- `POST /auth/login` — email + password → verify against the stored hash, return an access token (+ refresh token)
- `POST /auth/refresh` — exchange a valid refresh token for a new access token
- `GET /auth/me` — returns the current user, requires a valid access token

Also build the middleware (`apps/backend/src/middleware/auth.js`) that verifies the JWT on protected routes and attaches `req.user`.

**Security basics that matter here, not just style points:**
- Never return `passwordHash` in any API response
- Access tokens short-lived (~15 min), refresh tokens longer (~7 days), both signed with separate secrets
- Rate-limit `/auth/login` if you have time (even a basic in-memory limiter) — stretch, not required

## Acceptance criteria
- [ ] Registering with an already-used email returns a clear `409` error, not a crash
- [ ] Login with wrong password returns `401`, doesn't leak whether the email exists
- [ ] A valid access token on `GET /auth/me` returns the user (minus `passwordHash`)
- [ ] An expired or missing token on any protected route returns `401`, not `500`
- [ ] Passwords are never stored or logged in plain text — verify by checking the database directly

## Resources
- [jsonwebtoken (npm) docs](https://www.npmjs.com/package/jsonwebtoken)
- [bcrypt (npm) docs](https://www.npmjs.com/package/bcrypt)
- [JWT.io — Introduction](https://jwt.io/introduction)
- [OWASP — Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) (skim, don't need to memorize — good to know what exists)

## Notes
Depends on `docs/issues/01-database-schema.md` (needs the `User` table). Pairs well with `docs/issues/03-auth-frontend.md` — good candidate for two people working opposite ends of the same feature and syncing on the request/response shape early.
