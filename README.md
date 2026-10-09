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

- `UI/Scripture Pod Pro Panel.html` — control panel UI
- `UI/Scripture Pod Pro_display.html` — output/display window

Notes:

- For full functionality (Electron APIs, local filesystem access, packaging), run via `npm start`.
- When using browser-only mode, some features (native menus, file dialogs, electron-specific modules) will be unavailable.

## Display on another computer

The Electron app can serve the display over the local network. Both computers must be on the same reachable network, and the control computer must remain running.

1. Start the desktop app with `npm start` or open the installed app.
2. In the control panel, open **Settings → Host Mode** and select **vMix**. This enables panel updates to be relayed to a remote display; the vMix integration itself does not need to be enabled.
3. In the same settings section, use **LAN Display URL**. Click **Refresh** after changing networks, then **Copy**.
4. Open the copied URL in a browser on the other computer.

The app also prints the current display URL to the terminal after its local HTTP and WebSocket servers start. The URL uses the control computer's current LAN IP, so it can change when that computer joins another network. Allow inbound TCP ports `5510` (display page) and `5511` (update relay) through the control computer's firewall. Do not expose these ports directly to the public internet.

This is a browser-based network display, not an NDI output stream. Both computers need browser access to the host computer; an NDI receiver will not discover this URL as an NDI source.

## Building installers (macOS/Windows/Linux)

Install dev dependencies (already in `package.json`) and run the appropriate script. Example (mac):

```bash
npm run dist:mac
```

The `build` section in `package.json` is configured for `electron-builder`.

On macOS, choose the target architecture explicitly when needed:

```bash
npm run dist:mac -- --arm64
npm run dist:mac -- --x64
```

Build Windows installers with `npm run dist:win` and Linux packages with `npm run dist:linux`. For reliable releases, build each target on its corresponding operating system.

## Project layout (important files)

- `UI/Scripture Pod Pro Panel.html` — main control panel
- `UI/Scripture Pod Pro_display.html` — renderer/display
- `js/` — application JavaScript modules used by the panel
- `electron/` — Electron bootstrap (main, preload, helpers)
- `electron/resources/` — app icon assets for macOS, Windows, and Linux
- `server/feedback-backend.js` — optional local feedback server

## Troubleshooting

- If `npm install` fails, ensure Node version is compatible and your environment can compile native modules.
- If Electron windows do not appear when running `npm start`, check the terminal for errors and ensure no other instance is locking required ports.
- If the remote display does not load, confirm both computers are on the same network, refresh the LAN URL, and allow TCP ports `5510` and `5511` through the host firewall.

## Contributing

Fork, make changes, and submit a pull request. Keep changes focused and include short tests or manual verification steps.
