# TARZO — React Clothing Storefront

A responsive, editorial-style clothing brand website built with **React 19, TypeScript, Next.js-compatible routing (Vinext), and Cloudflare Workers**. The hosted site uses a Cloudflare D1 database for product inquiries and launch email signups.

## Pages

| Route | Purpose |
| --- | --- |
| `/` | Video-led homepage, featured styles, brand story, newsletter and editorial teasers |
| `/shop` | Searchable and sortable product catalogue with category filters and quick views |
| `/collections` | Editorial category showcases |
| `/products/[slug]` | Product gallery, size options, details and inquiry bag |
| `/about` | Brand story and values |
| `/contact` | WhatsApp contact and introductory FAQs |
| `/journal` | Original style guides and editorial articles |
| `/journal/[slug]` | Individual, SEO-friendly article pages |
| `/size-guide` | How-to-measure guidance for shirts and T-shirts |
| `/faq` | Frequently asked questions |
| `/privacy` | Privacy information |

## Getting started

Requirements: Node.js 22.13 or later, and a Cloudflare-compatible local runtime for backend features.

```bash
npm install
npm run dev
```

To produce a production build:

```bash
npm run build
```

The project uses a hosted Site-specific build integration. The `.openai/hosting.json` file declares the `DB` D1 binding; order inquiries and launch emails require that binding and the SQL migration in `drizzle/`.

## Editing TARZO content

- **Products, descriptions, sizes and images:** `lib/catalog.ts`
- **Original journal articles:** `lib/journal.ts`
- **Homepage, product cards, cart and site navigation:** `components/tarzo-store.tsx`
- **Shop, collections, about and contact:** `components/site-pages.tsx`
- **Journal, fit guide and FAQs:** `components/extra-pages.tsx`
- **Theme and responsive styling:** `app/globals.css`
- **WhatsApp chat destination:** `app/contact/whatsapp/route.ts`
- **SEO sitemap:** `app/sitemap.ts`

## Backend

- `POST /api/orders`: validates and records a selected product inquiry (no checkout payment).
- `POST /api/subscribe`: validates an email and adds it to the launch list.
- `GET /contact/whatsapp`: redirects visitors to TARZO's configured WhatsApp chat.

The phone number is deliberately **not displayed** in the website footer. It is configured in the server redirect route.

## Before accepting paid orders

Product photography and descriptions currently represent an **editorial preview collection**. TARZO should approve final garment photography, sizes, material composition, prices, inventory, shipping terms, returns policy and payment processes before launching a paid checkout. No payment collection is implemented here.

## Domain and indexing

The Site currently has a platform URL, and `weartarzo.com` has been requested as a custom domain. Activation depends on domain ownership and DNS verification. Update `siteUrl` in `lib/catalog.ts` and confirm SEO canonical URLs and Search Console indexing **only when the custom domain is verified and live**.

## Notes

- Product photos and the hero motion video are in `public/images/` and `public/videos/`.
- The 2560×1080 hero MP4 is a subtle camera-motion treatment of a still editorial image, not live-action footage.
- The code intentionally uses plain anchor links for reliable navigation on the deployed Vinext adapter.
