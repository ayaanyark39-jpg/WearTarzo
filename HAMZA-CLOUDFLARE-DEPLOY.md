# TARZO for Hamza — Cloudflare deployment package

This is a separately build-tested Cloudflare Workers + D1 edition of TARZO. It is a **new deployment**, not a cross-account transfer of the original Sites project. The old Papa-account Site and its records remain untouched.

## Account and privacy

1. Create/sign into a Cloudflare account with **humzacrypto@gmail.com**. Enable two-factor authentication. Do not paste the password or verification codes into ChatGPT.
2. This package defaults to **workers_dev: false**, so deploying it will **not** make it accessible at a public workers.dev URL until you intentionally enable a route/domain or adjust that setting. A new public URL is a separate launch decision.
3. The source contains **no production customer database records**, no Site credentials, and no admin passphrase.

## Install and connect

Use Node.js 22 or newer. In the unzipped project directory:

```bash
npm ci
npx wrangler login
npx wrangler d1 create wear-tarzo-db
```

The D1 command prints a UUID. Replace the placeholder `database_id` in `wrangler.jsonc` with that exact UUID. The database binding name must remain `DB`.

Apply the supplied schema migrations **to your new database only**:

```bash
npx wrangler d1 migrations apply wear-tarzo-db --remote --config wrangler.jsonc
```

## Build and deploy privately

```bash
npm run build
npx wrangler deploy --config dist/server/wrangler.json
```

After the Worker exists, set a strong new owner passphrase using Cloudflare's secret input (the command prompts for it):

```bash
npx wrangler secret put TARZO_ADMIN_KEY --name wear-tarzo
```

Do not put a passphrase in the source, a chat message, or an environment file. The application expects at least 24 characters. Its admin dashboard remains unavailable if the secret is missing.

## Prepare the eventual public URL

The package intentionally uses `https://tarzo.example.invalid` as a nonworking placeholder for canonical URLs and product links. When you have an actual URL on the new Cloudflare account, set `VITE_TARZO_SITE_URL` to its full HTTPS origin **before building**. Example:

```bash
VITE_TARZO_SITE_URL=https://your-real-domain.example npm run build
npx wrangler deploy --config dist/server/wrangler.json
```

Only then enable a domain/route (or workers.dev) with the desired access policy. Cloudflare deployment does not automatically make a Worker private to its owner if a public route is enabled; use Cloudflare Access or keep public routes disabled until launch.

## Transfer the live business records separately

The original Papa-account D1 database has `order_inquiries` records. The `member_signups` and `subscribers` tables were empty when last inspected. **Do not abandon those order records.** Export/import them only once the destination DB is created and authenticated, using a private secure transfer. The request counters in `request_counters` are ephemeral; do not transfer those.

Before switching off the old private Site:

- Verify site pages, responsive layout and all embedded videos;
- Verify product selection and WhatsApp chat link;
- Verify signup/newsletter submit successfully to the **new** D1 database;
- Verify the admin login secret is configured and dashboard is restricted;
- Confirm existing order records migrated as intended;
- Confirm security headers and the new hosting account's MFA.

The original Papa-account URL cannot automatically be reassigned to a separate Cloudflare account. A new hostname or a domain you own is needed for the new deployment.
