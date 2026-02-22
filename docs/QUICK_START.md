# QUICK START (Preview)

This gets you running quickly with temporary tunnel URLs.

## 1) Start relay on your OpenClaw host

- Relay should expose at least:
  - `GET /health`
  - `GET /cron/list`
  - `POST /cron/add`
  - `PUT /cron/update/:id`
  - `DELETE /cron/delete/:id`

## 2) Start a quick Cloudflare tunnel

```bash
cloudflared tunnel --url http://localhost:19002
```

Copy the generated `https://*.trycloudflare.com` URL.

## 3) Point frontend API to the tunnel URL

In frontend config (or `index.html`), set:

```js
const API = 'https://your-trycloudflare-url.trycloudflare.com';
```

## 4) Open frontend from Telegram/web

- Telegram Mini App or browser can now read/write cron via relay.

## 5) Verify

- Open app and ensure cron list loads.
- Try add/edit/delete one cron item.
