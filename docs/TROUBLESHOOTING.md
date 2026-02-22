# Troubleshooting

## 1) White screen / page not loading

- Confirm latest `index.html` deployed
- Wait 1–2 minutes for Pages deployment
- Hard refresh browser cache

## 2) Cron list load failed

Check relay:

```bash
curl -s http://localhost:19002/health
```

Check tunnel:

```bash
curl -s https://<your-tunnel-domain>/health
```

## 3) Tunnel URL expired (quick mode)

Symptoms: 530 / timeout.

Restart:

```bash
pkill -f cloudflared
cloudflared tunnel --url http://localhost:19002
```

Update frontend API URL afterward.

## 4) Add/Edit/Delete has no effect

- Check relay logs
- Check write permission on cron store file
- Validate relay route paths

## 5) Mobile button weird behavior

- Ensure you are opening hosted page, not Telegram file preview
- Test in Safari directly

## 6) Rollback

- Restore cron store backup file
- Revert frontend commit in GitHub
