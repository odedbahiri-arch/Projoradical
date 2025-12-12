## Portal to the Future – Runbook

This project serves a Webflow export plus an embedded Three.js “Meatballs2” scene (Vite build). Use this guide to avoid the blank/old iframe issue.

### Normal (final) view
1. From repo root: `npm install` (only if `node_modules` is missing).
2. Run: `npm run dev`.
3. Open: `http://localhost:8000/`. The iframe loads `meatballs2/dist/index.html`. Only one process needed.

### Update Meatballs2 content (embedded)
1. Edit files in `meatballs2/src/` (HTML/JS/CSS).
2. In `meatballs2`: `npm install` once (if needed), then `npm run build`.
3. Refresh `http://localhost:8000/` (root dev server from `npm run dev`). The iframe shows the new build.

### Live editing workflow (two processes)
- Terminal A (root): `npm run dev` → serves main site at `http://localhost:8000/`.
- Terminal B (`meatballs2`): `npm run dev` → Vite dev server at `http://localhost:3000/` for instant changes.
- Preview live changes at `http://localhost:3000/`. When satisfied, run `npm run build` in `meatballs2`, then refresh `http://localhost:8000/` to update the embed.

### Important settings
- `meatballs2/vite.config.js` has `base: './'` so built assets load correctly when embedded.
- The iframe in root `index.html` points to `meatballs2/dist/index.html`.

### Common pitfalls
- Blank or old iframe: forgot to rebuild after edits → run `npm run build` in `meatballs2`.
- 404s for assets: ensure `base: './'` stays set and iframe src remains `meatballs2/dist/index.html`.
- Missing dependencies after cleanup: run `npm install` in both root and `meatballs2`.
- Stale cache: hard refresh the browser if things look unchanged.

### Quick commands
- Root dev server: `npm run dev`
- Meatballs2 rebuild: `cd meatballs2 && npm run build`
- Meatballs2 live dev: `cd meatballs2 && npm run dev` (for preview only)

