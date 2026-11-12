# TARZO — Clothing Store Website

TARZO full-stack React / TypeScript storefront source code, prepared for Visual Studio Code and GitHub.

**Read [`START-HERE-GITHUB.md`](START-HERE-GITHUB.md) before setup.**

## Local quick start

- Install Node.js **22.13+** and Git.
- Open this folder in Visual Studio Code.
- Run `npm ci`, then `npm run dev`.
- Open the local address printed in the terminal.

For production hosting, follow [`HAMZA-CLOUDFLARE-DEPLOY.md`](HAMZA-CLOUDFLARE-DEPLOY.md).

### Contents

- `app/`: pages, API routes, global CSS.
- `components/`: storefront, product and reusable UI components.
- `lib/`, `hooks/`: shared logic.
- `db/`, `drizzle/`: schema and migrations (no customer data exported).
- `public/images/`, `public/videos/`: store images and campaign videos (full archive only).
- `worker/`, `wrangler.jsonc`: Cloudflare Worker entrypoint/configuration.
- `package.json`, `package-lock.json`: dependencies.

### Snapshot clarification

This is the **last complete source archive available in this conversation's working files**, saved during the November 11, 2026 development. It is a **v18-era archive**. It is **not verified as an exact copy of the current live TARZO project**; later updates (including newer promotional/header changes) may be absent. Do not overwrite the existing live site with this snapshot until comparing with the latest Sites project.

No live deployment, private user data, or authentication credentials are included.
