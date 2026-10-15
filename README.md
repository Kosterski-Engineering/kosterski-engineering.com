# kosterski-engineering.com
Main KE website — static placeholder ("hello world") page.

Plain HTML + CSS, no build step. Open `index.html` in a browser or serve the folder:

```
python3 -m http.server 8000
```

Structure:
- `index.html` — landing page
- `favicon.svg` — Signal Orange symbol on an Ink tile
- `assets/style.css` — brand tokens (colours, IBM Plex type) and layout
- `assets/fonts/` — IBM Plex Sans / Mono (woff2, self-hosted)
- `assets/img/symbol_accent.svg` — logo symbol

Open items: contact e-mail placeholder in `index.html`, full horizontal logo files from the brand package (`01_logo/`).
