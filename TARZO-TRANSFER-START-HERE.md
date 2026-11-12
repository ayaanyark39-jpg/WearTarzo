# TARZO — Transfer-ready website source

This archive is a portable copy of the TARZO v13 website. It includes the complete frontend, bundled videos/images, server routes, database schema/migrations, and security changes. It intentionally **excludes** the original Sites repository, cached builds, credentials and the original `.openai/hosting.json` identity so it cannot automatically overwrite the existing Papa-account Site.

## To deploy under Hamza's own account

1. Sign in to the destination hosting account (`humzacrypto@gmail.com`). For ChatGPT Sites, that account needs Site creation access (currently Plus, Pro or an eligible Work workspace). If the account does not have Sites, choose and authorize another compatible host first.
2. Create a **new private** hosted Site in the destination account. Do not reuse the old Papa-account project ID.
3. Import/adapt this source into the new Site, preserving `public/` assets and all app pages. Generate a fresh `.openai/hosting.json` from the **new** Site identity and set its `d1` binding to `DB` (and `r2` to `null` unless new storage is added).
4. Recreate the D1 database schema using the committed `drizzle/` SQL migrations. Site setup should apply migrations before production traffic.
5. Configure a **new** secret `TARZO_ADMIN_KEY` on the destination through its secret settings; do not copy an old secret into chat or code. Use at least 24 random characters.
6. In `lib/catalog.ts`, replace the old live `siteUrl` with the **new** URL. Review canonical links, email/social contact settings and any environment-specific references. Keep WhatsApp orders pointing to the intended business number.
7. Build and test all pages, video playback, customer signup, the private admin dashboard, and WhatsApp order links before publishing or changing domains.

## Database records: separate migration

This source archive does **not** contain production customer records. The original database has `order_inquiries`, `member_signups`, `subscribers` and request security counters. An inspection showed that order inquiries contain records; the other two customer tables were empty at inspection. **Do not lose existing order inquiries.** Export these records through an owner-authorized, secure route only after the new private database exists, then import them into the new database. Do **not** migrate rate-limit counters; they are temporary.

Never publish a raw customer-data export, commit it to a repository, or send it to an unrelated account. Confirm access to the destination account before the data move. Keep the original private Site intact until the new Site and records are verified. Switching URL ownership or deleting the old Site is a separate final step.

## Important hosting limitations

Cross-workspace Sites ownership is not automatically transferred by moving source code. A new deployment under Hamza's account has a new Site identity and normally a different public URL. Owner controls and the Site's database are provisioned separately. ChatGPT Sites currently supports building in Plus/Pro or eligible workspaces; a Free personal account may need a plan with Sites or another hosting provider.
