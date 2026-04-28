# Scripture Pod Pro

This repository contains the control Panel and Display for Scripture Pod Pro (a Bible / lyrics projection tool). It can be run in-browser or as an Electron desktop app.

## Requirements
- Node.js (v18+ recommended)
- npm (bundled with Node)
- Optional: Electron build tools if packaging an app (`electron-builder`)

## Quick start (development)

1. Install dependencies:

```bash
cd "$(dirname "$0")"
npm install
```

2. Run the Electron desktop app (launches the panel and display in windows):

```bash
npm start
```

3. Run only the feedback backend (optional):

```bash
npm run feedback:server
```

## Run in a browser (panel + display)

You can open the following files directly in a modern browser for quick testing (not packaged):

- `Scripture Pod Pro Panel.html` — control panel UI
- `Scripture Pod Pro_display.html` — output/display window

Notes:
- For full functionality (Electron APIs, local filesystem access, packaging), run via `npm start`.
- When using browser-only mode, some features (native menus, file dialogs, electron-specific modules) will be unavailable.

## Building installers (macOS/Windows/Linux)

Install dev dependencies (already in `package.json`) and run the appropriate script. Example (mac):

```bash
npm run dist:mac
```

The `build` section in `package.json` is configured for `electron-builder`.

## Project layout (important files)

- `Scripture Pod Pro Panel.html` — main control panel
- `Scripture Pod Pro Display.html` — renderer/display
- `js/` — application JavaScript modules used by the panel
- `electron/` — Electron bootstrap (main, preload, helpers)
- `server/feedback-backend.js` — optional local feedback server

## Troubleshooting
- If `npm install` fails, ensure Node version is compatible and your environment can compile native modules.
- If Electron windows do not appear when running `npm start`, check the terminal for errors and ensure no other instance is locking required ports.

## Contributing
Fork, make changes, and submit a pull request. Keep changes focused and include short tests or manual verification steps.
