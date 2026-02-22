# OpenClaw Studio Bootstrap

Mobile-first bootstrap kit for managing OpenClaw from Telegram Mini App and web.

## What this project is

OpenClaw Studio Bootstrap helps you quickly set up a cross-device control panel for your OpenClaw runtime, including:

- Cron management (list/add/update/delete)
- Model/status controls (planned)
- Session/tools panel (planned)

Architecture:

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

---

## Repository structure

```text
frontend/        # Mini App / web UI
relay/           # API bridge to OpenClaw
scripts/         # install, doctor, run scripts
docs/            # setup, security, troubleshooting
```

---

## Security notes

- Do not expose write APIs without access control
- Prefer Cloudflare Access for protected endpoints
- Keep secrets/tokens out of frontend code
- Enable operation audit logging in Relay

---

## License

MIT
