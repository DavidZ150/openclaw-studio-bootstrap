# Stable Setup with Cloudflare Named Tunnel

Use this for production-like stable access.

## Prerequisites

- Domain managed in Cloudflare (zone status: Active)
- `cloudflared` installed on OpenClaw host
- Relay running at `http://localhost:19002`

## 1) Login and create named tunnel

```bash
cloudflared tunnel login
cloudflared tunnel create openclaw-cron
```

## 2) Route DNS

```bash
cloudflared tunnel route dns openclaw-cron cron.yourdomain.com
```

## 3) Create config file `~/.cloudflared/config.yml`

```yaml
tunnel: openclaw-cron
credentials-file: /Users/<you>/.cloudflared/<TUNNEL_ID>.json
ingress:
  - hostname: cron.yourdomain.com
    service: http://localhost:19002
  - service: http_status:404
```

## 4) Run tunnel

```bash
cloudflared tunnel run openclaw-cron
```

## 5) Verify

```bash
curl -s https://cron.yourdomain.com/health
```

Expected: `{"status":"ok"}`

## 6) Frontend API

Set frontend API to:

```js
const API = 'https://cron.yourdomain.com';
```

## 7) Recommended hardening

- Enable Cloudflare Access on `cron.yourdomain.com`
- Restrict to your email identities
- Add relay + tunnel process supervision (launchd/systemd)
