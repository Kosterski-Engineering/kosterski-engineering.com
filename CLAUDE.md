# kosterski-engineering.com

Company website of Kosterski Engineering sp. z o.o. Static HTML + CSS, no build step, hosted on GitHub Pages.

## Working rules

- `main` is production: every merge to `main` publishes the site. Never push or merge to `main` yourself unless the user explicitly asks for it in this session.
- Work on the session branch. When a change is ready, commit, push and open a pull request to `main` without being asked; the PR gets a preview link (see below). Give the user the PR link.
- Before opening or updating a PR, check the page in Chromium at desktop (1440 px) and mobile (390 px) width and show the user the screenshots.
- Apply the `kosterski-brand` skill to every change: original logo and favicon files from the brand pack (never redrawn), `--ke-` tokens from `assets/tokens.css`, IBM Plex, brand claims in their roles.
- Website copy is in English. No invented facts, figures, clients or certifications; mark unknowns as `[placeholders]`.
- Use relative paths for links and assets, so pages work both on the custom domain and under `/preview/<uuid>/`.
- Do not edit `assets/tokens.css`; it is copied from the brand pack (`07_web/tokens.css`).

## Previews

`.github/workflows/pages.yml` deploys `main` and every open PR from this repository. Each PR is published at `<site>/preview/<random UUID>/`; the bot posts and updates the link as a comment on the PR. The link stays the same across pushes and disappears after the PR is merged or closed. Previews are unlisted (noindex), not access-protected.

Files not published: `README.md`, `CLAUDE.md`, `.github/`, `.gitignore`, `.claude/` (the `EXCLUDE` list in the workflow).

## Local preview

```
python3 -m http.server 8000
```
