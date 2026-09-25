---
title: "Auth frontend — login, register, session"
labels: [frontend, auth]
---

## Skills you'll practice
Controlled forms, client-side validation, storing auth state, protected routes in React.

## Description
Build:

- `/register` and `/login` pages with basic client-side validation (required fields, password length, matching email format)
- An `AuthContext` (`apps/frontend/src/context/AuthContext.jsx`) that holds the current user + access token, exposes `login()`, `register()`, `logout()`
- Token storage: use an in-memory variable + refresh-on-load, or `localStorage` for the access token if that's simpler for v1 — note the tradeoff in your PR description (localStorage is readable by any script on the page, which matters if this ever handles real data)
- A `ProtectedRoute` wrapper component that redirects to `/login` if there's no user
- A simple navbar that shows "Log in" vs. the user's name + "Log out" depending on auth state

## Acceptance criteria
- [ ] Registering with a bad email or short password shows an inline error, no page reload
- [ ] Successful login redirects to the homepage and the navbar updates
- [ ] Refreshing the page keeps the user logged in (token persisted somewhere, session restored on load)
- [ ] Visiting a protected route (e.g. `/checkout`) while logged out redirects to `/login`
- [ ] Logging out clears the token and redirects home

## Resources
- [React docs — Forms](https://react.dev/reference/react-dom/components/input)
- [React Router — Protected routes pattern](https://reactrouter.com/en/main/start/tutorial)
- MDN — [Storage quotas and eviction criteria](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) (background on why localStorage vs. memory is a real tradeoff, not just style)

## Notes
Depends on `docs/issues/02-auth-api.md` for the actual endpoints — agree on the request/response JSON shape with whoever's building that before you start, so you're not blocked waiting on their PR to merge first.
