# TeamCart — frontend

React + Vite + Tailwind CSS.

## Setup

This folder is intentionally empty except for this README — whoever picks up `docs/issues/00-scaffolding.md` should generate the real scaffold with the official CLI rather than hand-copying one, so it starts from current, correctly-versioned dependencies:

```bash
cd apps/frontend
npm create vite@latest . -- --template react
npm install
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Then point `src/index.css` at Tailwind's layers (`@tailwind base; @tailwind components; @tailwind utilities;`) and set `content` in `tailwind.config.js` to `["./index.html", "./src/**/*.{js,jsx}"]`.

```bash
npm run dev   # http://localhost:5173
```

## Suggested folder layout inside `src/`

```
src/
├── main.jsx
├── App.jsx
├── pages/            # ProductList, ProductDetail, Cart, Checkout, Login, Register, Admin
├── components/        # shared UI pieces (ProductCard, Navbar, CartIcon, ...)
├── context/           # AuthContext, CartContext
├── api/               # fetch wrappers for the backend (one file per resource)
└── hooks/
```

## Talking to the backend

The backend runs on `http://localhost:4000` by default (see `apps/backend/.env.example`). Point fetch calls there in dev, and put the base URL in an env variable (`VITE_API_URL`) rather than hardcoding it, so it's easy to swap for a deployed API URL later.

## Whose issue is this?

`docs/issues/03-auth-frontend.md` and `docs/issues/05-catalog-frontend.md` are the two frontend-heavy issues to start with — both assume the scaffolding above is already done.
