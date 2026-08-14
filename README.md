# allanronalddones.com

Personal professional site for **Allan Ronald Dones** — Senior Mechanical Engineer, rotating equipment and mechanical packages.

Static site. No build step, no dependencies, no backend. What's in this repo is what gets served.

## Structure

```
index.html                            Main page (single page, anchored sections)
404.html                              Not-found page
assets/site.css                       Shared stylesheet — site pages only
assets/allan-dones.jpg                Portrait (480×480)
tools/*.html                          Self-contained engineering tools, one file each
robots.txt  sitemap.xml  _headers     Crawler, sitemap, security headers
DEPLOY.md                             Deployment and maintenance guide
```

## Architecture

Site pages share `assets/site.css`. **Tools are deliberately self-contained** — each carries its own inline CSS and JS so it stays portable: linkable, emailable, and usable offline.

The trade-off is accepted knowingly: design tokens exist in both `site.css` and inside each tool, so a palette change requires updating each tool by hand.

## Local preview

```bash
python -m http.server --directory . 8975
```

Then open <http://localhost:8975/index.html>.

## Deploying

See [DEPLOY.md](DEPLOY.md). Cloudflare Pages, connected to this repo — every push to `main` redeploys automatically.
