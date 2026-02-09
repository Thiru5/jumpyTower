Valentine Tower — Hosting on Render (Static Site)

This project is a small HTML/JavaScript game (Electron desktop + renderer). To host the renderer (the playable web version) on Render as a static site follow the steps below.

Important files
- `index.html` — the game entry point (already at repo root)
- `public/` — put your assets here (music.mp3, jump.mp3, head images like `girl.png`, `boy.png`, `girl-jump.png`, etc.)

Quick checklist before deploying
1. Make sure `public/` exists at the repository root and contains your audio/images.
2. Commit all files and push to GitHub (or another Git provider connected to Render).

Option 1 — Deploy as a Static Site on Render (recommended)
1. Push your repo to GitHub.
2. Sign in to https://render.com and click "New" → "Static Site".
3. Connect your GitHub repo and select the branch you want to deploy.
4. In the Render site settings set:
   - Build Command: leave empty (or set to `echo "no build"`).
   - Publish Directory: `/` (project root).
5. Create the site. Render will publish your `index.html` and the `public/` assets.

Notes
- Asset paths in `index.html` use `public/...` (for example `public/music.mp3`). Those files must exist at `public/` in your repo root so they are available at `https://<your-site>/public/music.mp3`.
- Audio autoplay may be blocked until a user gesture; the game already falls back to starting music on the first click/keydown.

Local testing
- Quick static server to test locally:
```bash
# from project root
npx serve .        # or `npx http-server .`
# then open the printed URL (e.g. http://localhost:5000)
```

Troubleshooting
- Missing assets (404): visit `https://<your-site>/public/music.mp3` to check direct availability.
- If you prefer a Node server, add a small `server.js` and use Render "Web Service" instead — ask me and I can add that file.

Render manifest
- This repo already contains `render.yaml` which configures a Static Site (publishPath `/`). You can import the repo into Render and use that manifest if you prefer.

If you want, I can:
- Create the `public/` folder and add placeholder assets (small test audio + placeholder head images) so you can verify deployment end-to-end.
- Add a tiny `server.js` alternative if you prefer hosting as a Web Service.
