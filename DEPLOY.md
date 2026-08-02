# Deploying allanronalddones.com

Static site. No build step, no backend, no dependencies. Whatever is in this folder is the site.

## Files

| Path | Purpose |
|---|---|
| `index.html` | Main page |
| `assets/site.css` | Shared stylesheet — **site pages only** |
| `tools/vertical-pump-evaluation.html` | Self-contained tool. Carries its own CSS/JS on purpose |
| `404.html` | Not-found page |
| `robots.txt` | Crawler directives + sitemap pointer |
| `sitemap.xml` | Two URLs. **Add an entry whenever a tool is added** |
| `_headers` | Security + caching headers. Cloudflare Pages / Netlify only |

## Recommended: Cloudflare Pages

1. Register **allanronalddones.com** at Cloudflare Registrar (at-cost pricing, no renewal markup).
2. Push this folder to a private GitHub repo.
3. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
4. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
5. Deploy, then **Custom domains** → add `allanronalddones.com` and `www.allanronalddones.com`.
6. Confirm HTTPS is active (automatic) and that `www` redirects to apex.

Drag-and-drop upload also works if you'd rather skip Git — same dashboard, "Upload assets".

## Alternative: GitHub Pages

Works, with one loss: **GitHub Pages ignores `_headers`**, so you get no CSP or security headers. Acceptable for a site with no user input, but Cloudflare Pages is the better default.

## Post-deploy checks

- [ ] `https://allanronalddones.com/` loads over HTTPS
- [ ] Tools card opens the pump tool
- [ ] Back-link in the tool returns to the site root
- [ ] `https://allanronalddones.com/nonsense` shows the styled 404
- [ ] `robots.txt` and `sitemap.xml` resolve
- [ ] Paste the URL into LinkedIn or WhatsApp — confirm the preview card shows title and description
- [ ] Open the AFEO verify link and confirm the register record displays correctly
- [ ] Check on a phone

## Adding a tool later

The Tools section is organised into four equipment categories: **Pumps**,
**Compressors**, **Gas Turbines**, and **Building Management & HVAC**.

1. Build it self-contained (own CSS/JS inline, no external requests).
2. Save to `tools/<slug>.html`.
3. Set its back-link `href="/"` and add `canonical` + `og:url`.
4. In `index.html`, find the matching `<div class="tool-cat">` block:
   - Replace that category's `.soon-strip` with a `<div class="grid-3">` containing
     an `<a class="card tool-card">`, or add a card to the existing grid.
   - Update the `.count` span — `<span class="count live">N available</span>`.
5. Add the URL to `sitemap.xml`.

To add a fifth category, copy any `.tool-cat` block and change the heading.

## Known maintenance debt

The design tokens exist in two places: `assets/site.css` and inline inside each tool. This is deliberate — it keeps tools portable — but it means **a palette change requires editing every tool by hand**. Budget for that when the design changes.
