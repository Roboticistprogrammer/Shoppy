# TeamCart — backend

Express REST API + PostgreSQL (via Prisma).

## Setup

```bash
cd apps/backend
cp .env.example .env
npm install
```

If this is the very first setup (no `package.json` yet beyond this scaffold), initialize it:

```bash
npm init -y
npm install express cors dotenv bcrypt jsonwebtoken
npm install -D prisma typescript ts-node-dev @types/node @types/express nodemon
npx prisma init   # creates prisma/schema.prisma — replace it with the one already in this folder
```

Whoever picks up `docs/issues/00-scaffolding.md` owns turning this into a real, running `npm run dev` — everyone else's issue builds on top of what that issue produces. Feel free to swap TypeScript for plain JS if the team decides that's a smaller first step; just say so in the scaffolding PR.

## Database

The Prisma schema in `prisma/schema.prisma` currently has only a `User` model as a starting point — `docs/issues/01-database-schema.md` covers designing the rest (`Product`, `Category`, `Order`, `OrderItem`, `CartItem`).

```bash
npx prisma migrate dev --name init   # applies schema.prisma to Postgres
npx prisma studio                    # visual browser for the database, http://localhost:5555
```

## Suggested folder layout inside `src/`

```
src/
├── index.js            # server entry point
├── routes/              # one file per resource (auth.js, products.js, cart.js, orders.js)
├── middleware/           # auth.js (JWT verification), errorHandler.js
├── controllers/          # request handlers, one per route file
├── prisma.js             # exported Prisma client instance
└── utils/
```

Nobody has to follow this exactly — it's a reasonable default so the first few issues don't each reinvent the folder structure.

## Environment variables

See `.env.example` in this folder. `DATABASE_URL` must point at the Postgres container from the root `docker-compose.yml` — with the default credentials that's:

```
DATABASE_URL="postgresql://teamcart:teamcart_dev_password@localhost:5432/teamcart"
```
