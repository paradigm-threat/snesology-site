# SNESology

SNES Music Player powered by [SongWalker](https://songwalker.net).

Play music using authentic Super Nintendo sound samples with the SongWalker music engine.

## Development

```bash
npm install
npm run dev
```

Opens at http://localhost:3001

## Build

```bash
npm run build
npm run preview
```

## Architecture

- **Vite + TypeScript** — Build tooling
- **Monaco Editor** — Code editor with SongWalker syntax highlighting
- **songwalker-js** — Audio playback and preset loading (WASM-powered)
- **snesology-library** — SNES game sample presets (GitLab Pages)

## Sample Library

Samples are loaded from the SNESology library:
https://snesology-daa154.gitlab.io/

The library contains instrument presets extracted from classic Super Nintendo games.

## License

MIT
