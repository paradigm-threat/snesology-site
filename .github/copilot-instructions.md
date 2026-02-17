# Copilot Instructions — snesology-site

## Project Overview

`snesology-site` is the browser-based Retro Music Composer and editor. It uses:
- **Monaco Editor** — code editing with SongWalker language support
- **songwalker-js** — shared npm package providing WASM bindings, preset loader, and preset browser
- **Vite** — build tooling and dev server
- **Preset Loader** — loads SNES sampler presets from `snesology-library` (hosted on GitLab)

## Key Files

- `index.html` — full single-page app (HTML + CSS inline)
- `src/main.ts` — app entry: Monaco setup, play/stop, song loading, preset browser
- `vite.config.ts` — Vite config with `VITE_LIBRARY_URL` pointing to GitLab-hosted library
- `public/songs/` — example `.sw` song files
- `public/logos/` — site logos and icons

## Dependency on songwalker-js

This site depends on the `songwalker-js` npm package for:
- WASM bindings (compile, render, core_version)
- PresetLoader and PresetBrowser classes
- SongPlayer class

### Dependency Rules

**Never commit `file:` references** in `package.json` to git. Local `file:../songwalker-js`
references are convenient for development but **must be replaced** with the published npm
version before committing (e.g., `"songwalker-js": "^0.1.4"`). `file:` paths break
Vercel/GitHub/GitLab deployments because the sibling repo is not available in CI.

When `songwalker-js` is updated:
1. Publish the new version of `songwalker-js` to npm
2. Update the version in this repo's `package.json`
3. Run `npm install` to update `package-lock.json`
4. Commit and push

### Local Development with file: reference

For rapid iteration, you can temporarily switch to a `file:` reference:
```bash
# In package.json, change to: "songwalker-js": "file:../songwalker-js"
npm install
npm run dev
```
**Remember to revert before committing.**

## Development

```bash
npm install
npm run dev     # starts Vite dev server on port 3001
npm run build   # production build
```

## GitHub Actions

No CI workflows exist yet. If workflows are added, verify them after pushing:
```bash
cd /home/ari/dev/snesology-site
gh run list --limit 3                # check recent runs
gh run watch <run-id>                # watch a running build
gh run view <run-id> --log-failed    # inspect failures
```

Iterate on any failures until the workflow passes.
