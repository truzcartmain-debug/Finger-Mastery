# Finger Training Master — Typing Trainer & High Court Stenographer Coach

A single-file, self-contained typing trainer: dashboard, muscle-memory drills,
pattern training, a custom drill builder, a curated paragraph library with a
strict never-repeat system, a High Court stenographer training mode, and full
progress tracking — all in one `index.html`, no build step required.

## Deploy on GitHub Pages (free hosting)

1. Create a new **public** repository on GitHub (e.g. `keystroke-trainer`).
2. Upload `index.html` from this folder to the repository (drag-and-drop on
   github.com works fine, or use `git push` — see below).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Under **Branch**, choose `main` and folder `/ (root)`, then **Save**.
6. Wait 1–2 minutes. Your app will be live at:
   `https://<your-username>.github.io/<repo-name>/`

### Deploying with git from the command line

```bash
git init
git add index.html
git commit -m "Deploy keystroke typing trainer"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

Then follow steps 3–6 above.

## Important: data storage

This app was originally built for Claude's artifact environment, which
provides a `window.storage` API for saving progress. That API does not exist
in a normal browser, so this build includes a small polyfill at the top of
`index.html` that transparently backs `window.storage` with the browser's
own `localStorage` instead. Everything works the same way — dashboard stats,
mistake history, settings, seen-passage tracking — it just lives in each
visitor's own browser rather than in Claude's storage.

Because of that:

- **Data is per-browser, per-device.** Progress won't sync across devices or
  browsers automatically.
- **Data can be cleared** if a visitor clears their browser's site data, or
  uses a private/incognito window (nothing will be saved at all there).
- **Data lives per-origin.** If you later move the app to a different domain
  or path, that counts as a new origin and progress won't carry over.

If you eventually want real multi-device sync, you'd need to swap the
polyfill for calls to a real backend (e.g. a small API + database), but for
personal use or sharing as-is, the localStorage version works out of the box
with zero configuration.

## Local preview

No build step needed — just open `index.html` directly in a browser, or serve
it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Browser support

Uses standard modern browser APIs (Web Audio for keyboard sounds, Chart.js
via CDN for progress graphs, CSS custom properties). Works in current
Chrome, Edge, Firefox, and Safari. Requires internet access on first load
for the Google Fonts and Chart.js CDN links.
