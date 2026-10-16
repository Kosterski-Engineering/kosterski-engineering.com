# kosterski-engineering.com

Company website of Kosterski Engineering sp. z o.o. Static HTML + CSS, no build step. The website is the `site/` folder; everything outside it (this file, `README.md`) is never published.

Hosted on Cloudflare Pages (same setup as the `aspice.ai` repo), see **Hosting** below.

## Working rules

- `main` is production: every merge to `main` publishes the site. Never push or merge to `main` yourself unless the user explicitly asks for it in this session.
- Work on the session branch. When a change is ready, commit, push and open a pull request to `main` without being asked; the PR gets a preview link (see below).
- After every push to a PR, wait for the Cloudflare deploy to finish, then check that the branch preview URL loads and shows the change (previews are behind Cloudflare Access, see **Hosting**).
- End every message that reports a change with two links, so the author can send them to reviewers:
  - `PR: <link to the pull request>`
  - `Preview: <Cloudflare branch preview URL>`
- While a PR waits for review, subscribe to its activity and schedule a check-in about 50 minutes after the last activity (`send_later`). On each check-in, re-check the PR state, the Cloudflare deploy and mergeability; act if something changed, otherwise re-arm silently. Stop after 3 check-ins in a row with nothing new, and cancel the check-in as soon as the PR is merged or closed.
- Merge a PR only when the user explicitly asks for it; use squash merge. After the merge, check that production shows the change, then reset the session branch to `main`.
- Before opening or updating a PR that changes the page, check it in Chromium at desktop (1440 px) and mobile (390 px) width and show the user the screenshots.
- Apply the `kosterski-brand` skill to every change: original logo and favicon files from the brand pack (never redrawn), `--ke-` tokens from `assets/tokens.css`, IBM Plex, brand claims in their roles.
- Website copy is in English. No invented facts, figures, clients or certifications; mark unknowns as `[placeholders]`.
- Use relative paths for links and assets, so pages work on the custom domain, and on `*.pages.dev`.
- Do not edit `site/assets/tokens.css`; it is copied from the brand pack (`07_web/tokens.css`).
- Before the site goes live on its domain, `site/_headers` keeps `X-Robots-Tag: noindex` and `site/index.html` keeps `<meta name="robots" content="noindex, nofollow">`. Remove both at launch.

## Hosting

**Cloudflare Pages**: project `kosterski-engineering-com`, connected to this repository, no build command, output directory `site`. Push to `main` → production at https://kosterski-engineering-com.pages.dev (custom domain not connected yet). Push to any other branch → preview at `<branch>.kosterski-engineering-com.pages.dev`: `/` in the branch name becomes `-` and the name is cut to 28 characters (e.g. `claude/compassionate-cray-6iux86` → `claude-compassionate-cray-6i`). The `cloudflare-workers-and-pages` bot may post the URL as a PR comment; if it does not, derive it from the branch name. Cloudflare serves `page.html` at `/page` (a request for `/page.html` gets a 308 redirect). `site/_headers` sets the HTTP headers.

Previews are protected by Cloudflare Access (production is public). To check a preview from a session, send the service token from the environment: `curl -H "CF-Access-Client-Id: $CF_ACCESS_CLIENT_ID" -H "CF-Access-Client-Secret: $CF_ACCESS_CLIENT_SECRET" <url>`. A 302 to `cloudflareaccess.com` means no token was sent; a 403 means the token is not allowed by a `Service Auth` policy on the application.

Preview deployments are not removed when a branch is deleted or a PR is closed; they stay behind Access until deleted in the Cloudflare dashboard (project → Deployments).

GitHub Pages is no longer used (workflow removed on 2026-10-16).

## Local preview

```
python3 -m http.server 8000 -d site
```
