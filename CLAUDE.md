# kosterski-engineering.com

Company website of Kosterski Engineering sp. z o.o. Static HTML + CSS, no build step. The website is the `site/` folder; everything outside it (this file, `README.md`, `.github/`) is never published.

Hosting is moving from GitHub Pages to Cloudflare Pages (same setup as the `aspice.ai` repo). During the transition both run in parallel, see **Hosting** below.

## Working rules

- `main` is production: every merge to `main` publishes the site. Never push or merge to `main` yourself unless the user explicitly asks for it in this session.
- Work on the session branch. When a change is ready, commit, push and open a pull request to `main` without being asked; the PR gets a preview link (see below).
- After every push to a PR, wait for the deploy run to finish and for the bot comment to show the new commit, then check that the preview URL loads and shows the change.
- End every message that reports a change with two links, so the author can send them to reviewers:
  - `PR: <link to the pull request>`
  - `Preview: <preview link from the bot comment>`
- While a PR waits for review, subscribe to its activity and schedule a check-in about 50 minutes after the last activity (`send_later`). On each check-in, re-check the PR state, the deploy run and mergeability; act if something changed, otherwise re-arm silently. Stop after 3 check-ins in a row with nothing new, and cancel the check-in as soon as the PR is merged or closed.
- Merge a PR only when the user explicitly asks for it; use squash merge. After the merge, check that production shows the change and that the preview is gone, then reset the session branch to `main`.
- Before opening or updating a PR that changes the page, check it in Chromium at desktop (1440 px) and mobile (390 px) width and show the user the screenshots.
- Apply the `kosterski-brand` skill to every change: original logo and favicon files from the brand pack (never redrawn), `--ke-` tokens from `assets/tokens.css`, IBM Plex, brand claims in their roles.
- Website copy is in English. No invented facts, figures, clients or certifications; mark unknowns as `[placeholders]`.
- Use relative paths for links and assets, so pages work on the custom domain, on `*.pages.dev` and under `/preview/<uuid>/`.
- Do not edit `site/assets/tokens.css`; it is copied from the brand pack (`07_web/tokens.css`).
- Before the site goes live on its domain, `site/_headers` keeps `X-Robots-Tag: noindex`. Remove that line at launch.

## Hosting

**Cloudflare Pages** (target): project `kosterski-engineering-com`, connected to this repository, no build command, output directory `site`. Push to `main` → production at https://kosterski-engineering-com.pages.dev (custom domain not connected yet). Push to any other branch → preview at `<branch>.kosterski-engineering-com.pages.dev` (`/` in the branch name becomes `-`; long names are shortened); the `cloudflare-workers-and-pages` bot posts the branch preview URL as a comment on the PR. `site/_headers` sets the HTTP headers (Cloudflare only).

**GitHub Pages** (until the cutover): `.github/workflows/pages.yml` deploys `site/` from `main` and every open PR from this repository. Each PR is published at `<site>/preview/<random UUID>/`; the bot posts and updates the link as a comment on the PR. The link stays the same across pushes and disappears after the PR is merged or closed. Previews are unlisted (noindex), not access-protected.

Until the cutover, the `Preview:` link in messages is the Cloudflare branch preview; mention the GitHub Pages preview only if Cloudflare's is not available. After the custom domain is live on Cloudflare, the workflow and GitHub Pages are removed (only with the user's approval).

## Local preview

```
python3 -m http.server 8000 -d site
```
