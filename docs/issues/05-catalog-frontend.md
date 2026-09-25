---
title: "Catalog frontend — browse, search, filter"
labels: [frontend]
---

## Skills you'll practice
Data fetching, loading/error/empty states, component composition, URL-driven state (search params).

## Description
Build:

- A product grid page (`/`) — fetches from `GET /products`, shows a card per product (image, name, price, "Add to cart")
- A search bar + category filter dropdown, both reflected in the URL as query params (so a search is shareable/bookmarkable and survives a refresh)
- Pagination controls (Next/Previous, or numbered pages) wired to the API's `page`/`limit`
- A product detail page (`/products/:id`)
- Proper loading state (skeleton or spinner, not a blank flash) and an error state if the API call fails — don't let a failed fetch silently show an empty grid

## Acceptance criteria
- [ ] Typing in the search box filters the grid (debounced, not firing on every keystroke)
- [ ] Selecting a category updates both the grid and the URL (`?category=electronics`)
- [ ] Loading state is visible during fetch, not just a flash of empty content
- [ ] A deliberately-broken API call (temporarily point `VITE_API_URL` somewhere wrong) shows a real error message, not a blank page
- [ ] Product detail page shows full description, price, stock, and an "Add to cart" button

## Resources
- [React docs — Fetching data](https://react.dev/learn/synchronizing-with-effects#fetching-data)
- [React Router — useSearchParams](https://reactrouter.com/en/main/hooks/use-search-params)
- Look up "debounce input react" — several small, well-explained patterns; no need for a library for this scale

## Notes
Depends on `docs/issues/04-catalog-api.md`. Good pairing candidate with whoever built that API, so response-shape assumptions get caught early.
