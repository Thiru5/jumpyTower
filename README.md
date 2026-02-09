Valentine Tower — Hosting on Render (Static Site)

This project is a small HTML/JavaScript game (Electron desktop + renderer). The playable web renderer can be hosted as a static site on Render.

Important files
- `index.html` — the game entry point (already at repo root)
- `public/` — contains assets used by the web build (music.mp3, jump.mp3, head images like `girl.png`, `boy.png`, `girl-jump.png`, etc.)

Quick checklist before deploying
1. Make sure `public/` exists at the repository root and contains your audio/images.
2. Commit all files and push to GitHub (or another Git provider connected to Render).

Deploy as a Static Site on Render (recommended)
1. Push your repo to GitHub.
2. Sign in to https://render.com and click "New" → "Static Site".
3. Connect your GitHub repo and select the branch you want to deploy.
4. In the Render site settings set:
   - Build Command: `echo "no build"` (a harmless no-op).
   - Publish Directory: `.` (project root).
5. Create the site. Render will publish your `index.html`, the `200.html` health page, and the `public/` assets.

Notes
- Asset paths in `index.html` use `public/...` (for example `public/music.mp3`). Those files must exist at `public/` in your repo root so they are available at `https://<your-site>/public/music.mp3`.
- Audio autoplay may be blocked until a user gesture; the game already falls back to starting music on the first click/keydown.

Quick local test
Run a simple static server from the project root and verify the site and assets load:
```bash
# from project root
npx http-server -p 5000
# then open http://localhost:5000 in a browser
```

Health check
- A small `200.html` was added at the repo root to make it easy to verify that the site is up.
- After deployment you can verify directly:
  - https://<your-site>/200.html
  - https://<your-site>/public/music.mp3

Render manifest
- This repo contains `render.yaml` configured for a static site. It now sets an explicit build command and publishes the project root.

If you want, I can:
- Add placeholder assets for a fully automated smoke test.
- Add a tiny `server.js` alternative if you prefer hosting as a Render Web Service instead of a Static Site.
