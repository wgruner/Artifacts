# Artifacts

A personal collection of self-contained HTML pages ("artifacts"), each a standalone trip-planning tool or similar, hosted via GitHub Pages directly from this repo. There is no build step, no framework, no package.json, and no server — each page is a single `.html` file with inline `<style>`/`<script>`, optionally pulling in a CDN library (e.g. Leaflet) or calling a public, CORS-friendly, no-key API directly from the browser (e.g. Open-Meteo).

## Constraints

- **Frontend-only.** The owner isn't hosting a backend yet, so features must run entirely client-side. Prefer no-key, CORS-enabled public APIs callable with a plain `fetch()`. If a data source requires a server-side key/proxy, treat that as a blocker to raise, not something to work around.
- **No build step.** Don't introduce bundlers, npm packages, or a `package.json` — these pages need to keep working as plain static files.
- **Self-contained pages.** Keep each artifact's CSS/JS inline in its own file rather than splitting into shared assets, unless asked to change that.

## Conventions

- `index.html` is a manually maintained listing page linking to every artifact, each with a short description. When adding, renaming, or removing an artifact page, update `index.html` to match.
- Name artifact files descriptively (`Agua_Piedra_to_Jicarita_Peak_Loop.html`), not with version suffixes (`..._v49.html`) — git history is the version record now, not the filename.
- When renaming/moving a tracked file, use `git mv` so history follows the file.
- This is a live GitHub Pages site. Commits to `main` deploy directly — no branches/PRs/gitflow here, the owner has said direct commits are fine when asked, but don't commit or push without being asked first.

## Testing changes locally

Opening a page via `file://` in the sandboxed browser tool renders it as a static snapshot — links to other local files are blocked, so `file://` isn't representative of the deployed behavior for interactivity or navigation testing. To test a page for real (JS execution, link clicks, live `fetch()` calls), serve the repo over local HTTP instead. This environment has no `python`/`node`/`npx` on PATH; a quick fallback is a `System.Net.HttpListener`-based static file server run via `Start-Process powershell -WindowStyle Hidden` (see any recent session transcript for the exact script) — kill the background process when done testing.
