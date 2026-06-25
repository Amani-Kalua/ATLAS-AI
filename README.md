# A.T.L.A.S.

**A**utonomous **T**ask & **L**earning **A**gent **S**ystem — a desktop AI assistant for macOS with a retro sci-fi HUD, built on Claude.

![status](https://img.shields.io/badge/platform-macOS-blue) ![status](https://img.shields.io/badge/built%20with-Electron-47848F)

[**Live demo (UI only, no backend)**](https://amani-kalua.github.io/ATLAS-AI/)

## What it does

ATLAS gives Claude full access to your Mac through a set of tools, wrapped in a glowing radar-HUD interface with voice in/out, live system stats, and persistent task tracking.

- **Chat with Claude** — ask anything, get tool-augmented answers
- **File operations** — read, write, move, delete, search files
- **Run shell commands** — automate anything from the terminal
- **Open apps** — launch any macOS application by name
- **Clipboard access** — read and write the clipboard
- **Task management** — `add task ...` / `show tasks` — persists to disk
- **Notes** — `note: ...` — saved as markdown to `~/Documents/ATLAS-Notes/`
- **Pomodoro timer** — `pomodoro` / `start focus session` — 25/5 work-break cycle with notifications
- **Voice input/output** — speech-to-text commands, spoken responses
- **Quick intents** — time, date, weather, web search, timers, reminders — answered instantly without a round trip to Claude
- **Live system telemetry** — RAM, battery, uptime, coordinates rendered right on the HUD

## Screenshot

The interface: a glowing radar core, real-time system readouts, a chat history sidebar, and a command bar — all styled like a spaceship console.

## Getting started

### Requirements

- macOS
- [Node.js](https://nodejs.org/) 18+
- An [Anthropic API key](https://console.anthropic.com/)

### Install & run

```bash
git clone https://github.com/Amani-Kalua/ATLAS-AI.git
cd ATLAS-AI
npm install
npm run electron
```

On first launch, ATLAS will prompt you for your Anthropic API key. It's stored locally on your machine (in Electron's app data folder) and is never sent anywhere except Anthropic's API.

### Run as a plain web server (no Electron)

```bash
ANTHROPIC_API_KEY=sk-ant-... npm start
```

Then open `http://localhost:3000`.

## How it's built

- **`main.js`** — Electron entry point; boots the local Express server and opens the app window
- **`server.js`** — Express backend; proxies chat to the Anthropic API, defines and executes tools (file system, shell, clipboard, tasks, notes), and serves system status
- **`public/index.html`** — the entire frontend: HUD, chat UI, voice recognition/synthesis, intent detection, and task/timer panels, in one file
- **`preload.js`** — exposes a minimal, safe IPC bridge for the API key flow

## Privacy & security

- Your API key never leaves your machine except to talk to `api.anthropic.com`.
- `run_shell` and file tools operate with your full user permissions — Claude can read, write, and delete files, and execute arbitrary shell commands on your behalf. Only grant access you're comfortable with.
- Tasks and notes are stored locally in `~/.atlas-data/` and `~/Documents/ATLAS-Notes/`.

## Building a distributable app

```bash
npm run build
```

Produces a `.dmg` installer in `dist/` via `electron-builder`.

## License

Personal project — no license specified yet.
