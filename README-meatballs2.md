## Meatballs2 Embed & Dev Quick Guide

Keep this handy when the iframe scene goes blank or shows old content.

### What’s here
- The root site (`index.html`, css/js/images/fonts) embeds `meatballs2/dist/index.html` in an iframe.
- `meatballs2` is a Vite project; `base: './'` is set so dist assets load correctly from the iframe.

### Normal (final) view
1. From repo root: `npm install` (only if `node_modules` is missing).
2. Run: `npm run dev`.
3. Open: `http://localhost:8000/`. The iframe uses the built `meatballs2/dist/index.html`. Only one process needed.

### Update meatballs2 content (embed)
1. Edit files in `meatballs2/src/` (HTML/JS/CSS).
2. In `meatballs2`: `npm install` once (if needed), then `npm run build`.
3. Refresh `http://localhost:8000/` (root dev server still from `npm run dev`). The iframe now shows the new build.

### Live editing workflow (two processes)
- Terminal A (root): `npm run dev` → serves main site at `http://localhost:8000/`.
- Terminal B (`meatballs2`): `npm run dev` → Vite dev server at `http://localhost:3000/` for instant changes.
- Preview live changes at `http://localhost:3000/`. When satisfied, run `npm run build` in `meatballs2`, then refresh `http://localhost:8000/` to update the embed.

### Common pitfalls
- Blank/old iframe: forgot to rebuild `meatballs2` after edits; run `npm run build`.
- Paths 404: ensure `base: './'` (already set) and iframe src stays `meatballs2/dist/index.html`.
- Missing deps after cleanup: run `npm install` in both root and `meatballs2`.
- Stale cache: hard refresh the browser if things look unchanged.

### Quick commands
- Root dev server: `npm run dev`
- Meatballs2 rebuild: `cd meatballs2 && npm run build`
- Meatballs2 live dev: `cd meatballs2 && npm run dev` (for preview only)

