# kosterski-engineering.com

Company website of Kosterski Engineering sp. z o.o. Static HTML + CSS, no build step, hosted on GitHub Pages.

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
- Use relative paths for links and assets, so pages work both on the custom domain and under `/preview/<uuid>/`.
- Do not edit `assets/tokens.css`; it is copied from the brand pack (`07_web/tokens.css`).

## Previews

`.github/workflows/pages.yml` deploys `main` and every open PR from this repository. Each PR is published at `<site>/preview/<random UUID>/`; the bot posts and updates the link as a comment on the PR. The link stays the same across pushes and disappears after the PR is merged or closed. Previews are unlisted (noindex), not access-protected.

Files not published: `README.md`, `CLAUDE.md`, `.github/`, `.gitignore`, `.claude/` (the `EXCLUDE` list in the workflow).

## Local preview

```
python3 -m http.server 8000
```
