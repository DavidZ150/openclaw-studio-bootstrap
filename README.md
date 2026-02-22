# OpenClaw Studio Bootstrap

Mobile-first bootstrap kit for managing OpenClaw from Telegram Mini App and web.

## What this project is

OpenClaw Studio Bootstrap helps you quickly set up a cross-device control panel for your OpenClaw runtime, including:

- Cron management (list/add/update/delete)
- Model/status controls (planned)
- Session/tools panel (planned)

It uses a simple architecture:

`Frontend (Mini App/Web) -> Relay API -> OpenClaw runtime`

---

## Why this exists

Managing OpenClaw directly on the host machine is powerful but not always convenient.
This project provides a practical way to control key functions from your phone (Telegram Mini App) and desktop browser.

---

## Current status

- ✅ Cron Studio connected mode (MVP)
- ✅ Relay API for cron operations
- ✅ Cloudflare tunnel quick mode support
- ⏳ Stable domain mode (named tunnel + fixed subdomain)
- ⏳ Model/Status/Sessions modules

See roadmap in docs (coming soon).

---

## Quick Start (Preview)

> Detailed setup docs will be added.  
> This is a high-level preview.

1. Run Relay API locally on your OpenClaw host
2. Expose Relay via Cloudflare Tunnel
3. Point frontend API URL to tunnel domain
4. Open frontend from Telegram/web

---

## Repository structure (planned)

```text
frontend/        # Mini App / web UI
relay/           # API bridge to OpenClaw
scripts/         # install, doctor, run scripts
docs/            # setup, security, troubleshooting
