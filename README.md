# Cypressholt: Website

A one-page site for Cypressholt, which provides Solo and self-directed 401(k) plan support from an
office in Houston, Texas. It's static with no dependencies, built with Node and hosted on
**Cloudflare** (Workers static assets via `wrangler.jsonc`, or Pages).

## Quick start

```bash
node build.mjs          # builds ./dist; checks internal links; lists missing info
STRICT=1 node build.mjs # pre-launch check (fails while placeholders remain)
```

## Deploy to Cloudflare

**Workers (current setup):** Workers & Pages → Create → Import a repository → this repo.
Build command `npm run build`, deploy command `npx wrangler deploy`. `wrangler.jsonc` serves `./dist`.
Every push to the branch redeploys automatically.

**Pages (alternative):** Build command `node build.mjs`, output directory `dist`.

Security headers and redirects live in `src/static/_headers` and `src/static/_redirects`, which
are copied into `dist/` and applied by Cloudflare. After the first deploy, set `site.url` in
`site.config.mjs` to the live address (or custom domain) so canonicals, the sitemap and the form's
thank-you redirect are correct.

## Contact form (n8n)

The meeting form posts to an **n8n Webhook**, and the n8n workflow routes each submission
(email, sheet, CRM) and redirects the visitor to `/thank-you/`. Put the webhook's production URL
in `form.webhookUrl` in `site.config.mjs`. Until then the form shows a "not connected yet" notice
and won't send. Setup steps: `docs/N8N-FORM-SETUP.md`.

## Office

**6201 Bonhomme Rd, Houston, TX 77036** (storefront office). Phone: **(346) 482-3236**.

## Structure

The homepage (`/`) holds every section, each reachable from the menu and the sticky section bar:
Services · How it works · Who does what · 401(k) basics · FAQ · About · Visit & contact (meeting form).
`/privacy-policy/`, `/terms/` and `/disclosures/` are separate pages under Texas law,
plus `/thank-you/` and `404.html`.

## Design

- **Palette:** bayou night `#1E2A22`, cypress green `#2F5D46` (buttons), russet `#9A4A22`, ochre `#E3B36A`, autumn `#E9A16E`, paper `#FAF8F3`
- **Type:** Merriweather (display) and Karla (text), both self-hosted
- **Logo:** an octagon badge with a bald cypress in autumn russet standing in bayou water (`src/brand.mjs`)
- **Hero:** night drone video around a downtown Houston tower (desktop only; phones get the poster image)

See `docs/` for the launch checklist, media sources, Search Console and Google Business Profile steps.
