# kosterski-engineering.com
Main KE website — company profile site (English).

Plain HTML + CSS, no build step. The website lives in `site/`; serve it with:

```
python3 -m http.server 8000 -d site
```

Structure:
- `site/index.html` — home: services, products, about, contact
- `site/sysassist/` — SysAssist product page, EN (`index.html`) and PL (`pl/index.html`), with its own CSS, fonts and brand files in `sysassist/assets/`. Moved here from the `aspice.ai` repo, which now redirects to it. No Google Analytics or cookie banner.
- `site/test-fleet.html` — test and prototype fleet management (draft)
- `site/legal-notice.html` — legal notice (Impressum)
- `site/privacy.html` — privacy policy (GDPR)
- `site/favicon.svg`, `site/favicon.ico`, `site/apple-touch-icon.png` — favicons from the brand pack
- `site/assets/tokens.css` — brand tokens from the brand pack (`07_web/tokens.css`, do not edit)
- `site/assets/style.css` — page layout, uses the `--ke-` tokens
- `site/assets/fonts/` — IBM Plex Sans / Mono (woff2, self-hosted)
- `site/assets/img/logo_horizontal_accent_dark_bg.svg` — horizontal logo for dark ground (brand pack 2026-10-14)
- `site/_headers` — HTTP headers for Cloudflare Pages

## Deployment

Hosting and previews are described in `CLAUDE.md` (section **Hosting**), together with the working rules for Claude Code sessions.

### Cloudflare Pages

Workers & Pages → Create → Pages → Connect to Git → `Kosterski-Engineering/kosterski-engineering.com`; project name `kosterski-engineering-com`, production branch `main`, framework preset None, build command empty, build output directory `site`. Branch previews are behind Cloudflare Access.
