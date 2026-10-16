# kosterski-engineering.com
Main KE website — static placeholder ("hello world") page.

Plain HTML + CSS, no build step. Open `index.html` in a browser or serve the folder:

```
python3 -m http.server 8000
```

Structure:
- `index.html` — landing page
- `favicon.svg`, `favicon.ico`, `apple-touch-icon.png` — favicons from the brand pack
- `assets/tokens.css` — brand tokens from the brand pack (`07_web/tokens.css`, do not edit)
- `assets/style.css` — page layout, uses the `--ke-` tokens
- `assets/fonts/` — IBM Plex Sans / Mono (woff2, self-hosted)
- `assets/img/logo_horizontal_accent_dark_bg.svg` — horizontal logo for dark ground (brand pack 2026-10-14)

## Deployment (GitHub Pages)

Every push to `main` deploys the site via `.github/workflows/pages.yml` (manual run: Actions → Deploy to GitHub Pages → Run workflow). Everything in the repository is published except `README.md`, `CLAUDE.md`, `.github/`, `.gitignore` and `.claude/`.

Previews: every open pull request from this repository is also published at `<site>/preview/<random UUID>/`. The link is posted as a comment on the PR, stays the same for later pushes and stops working after the PR is merged or closed. Previews are unlisted (noindex, nofollow) but not password-protected. Until the official launch, production is also `noindex, nofollow` (meta tag in `index.html`).

Working rules for Claude Code sessions are in `CLAUDE.md`.

One-time setup in the repository:
1. Settings → Pages → Build and deployment → Source: **GitHub Actions**.
2. Custom domain (optional): Settings → Pages → Custom domain → `kosterski-engineering.com`, then at the DNS provider:
   - apex `kosterski-engineering.com`: A records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` (and AAAA `2606:50c0:8000::153` … `8003::153`),
   - `www`: CNAME `kosterski-engineering.github.io`.
   After DNS check passes, enable **Enforce HTTPS**.
