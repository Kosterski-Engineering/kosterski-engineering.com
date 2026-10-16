# kosterski-engineering.com
Main KE website — static placeholder ("hello world") page.

Plain HTML + CSS, no build step. The website lives in `site/`; serve it with:

```
python3 -m http.server 8000 -d site
```

Structure:
- `site/index.html` — landing page
- `site/favicon.svg`, `site/favicon.ico`, `site/apple-touch-icon.png` — favicons from the brand pack
- `site/assets/tokens.css` — brand tokens from the brand pack (`07_web/tokens.css`, do not edit)
- `site/assets/style.css` — page layout, uses the `--ke-` tokens
- `site/assets/fonts/` — IBM Plex Sans / Mono (woff2, self-hosted)
- `site/assets/img/logo_horizontal_accent_dark_bg.svg` — horizontal logo for dark ground (brand pack 2026-10-14)
- `site/_headers` — HTTP headers for Cloudflare Pages

## Deployment

Hosting and previews are described in `CLAUDE.md` (section **Hosting**), together with the working rules for Claude Code sessions.

### Cloudflare Pages (target)

Workers & Pages → Create → Pages → Connect to Git → `Kosterski-Engineering/kosterski-engineering.com`; project name `kosterski-engineering-com`, production branch `main`, framework preset None, build command empty, build output directory `site`.

### GitHub Pages (until the cutover)

`.github/workflows/pages.yml` publishes `site/` from `main` and from every open pull request (at `<site>/preview/<random UUID>/`, link posted as a PR comment). Previews are `noindex, nofollow`; until the official launch production is too (meta tag in `site/index.html`). Repository setting: Settings → Pages → Build and deployment → Source: **GitHub Actions**.
