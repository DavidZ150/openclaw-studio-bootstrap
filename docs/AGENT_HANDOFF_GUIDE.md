# AGENT HANDOFF GUIDE (High-Density)

This document is for AI agents/contributors who need to take over this project and deliver working results fast.

## 1) Objective
Build a cross-device OpenClaw control studio (Telegram Mini App + Web) that can manage core runtime functions remotely, starting with Cron and expanding to model/status/sessions.

## 2) Scope / Non-scope
### In scope
- Frontend control UI (mobile-first, web-compatible)
- Relay API on host machine
- Tunnel exposure for remote access
- Security baseline (access control + auditability)

### Out of scope
- Direct exposure of raw host shell to frontend
- Storing sensitive keys in frontend
- Broad, unrestricted filesystem writes

## 3) Canonical architecture
`Frontend -> Relay API -> OpenClaw runtime`

- Frontend: Telegram Mini App or browser UI
- Relay: request validation + mapping + audit
- OpenClaw runtime: actual cron/session/model operations

## 4) Current state snapshot
- Repo has README + setup docs.
- MVP cron relay approach validated.
- Quick tunnel works but URL rotates.
- Stable domain setup blocked by registrar ownership recovery in user environment.

## 5) Required reading order for takeover
1. `README.md`
2. `docs/QUICK_START.md`
3. `docs/STABLE_SETUP_CLOUDFLARE.md`
4. `docs/TROUBLESHOOTING.md`
5. (If available externally) local project notes about cron relay implementation.

## 6) Delivery phases
### Phase A: MVP (already targeted)
- cron list/add/update/delete working from mobile UI.

### Phase B: stable networking
- named tunnel + fixed domain + protected access.

### Phase C: module expansion
- model/status pages
- sessions/tools panel

### Phase D: production hardening
- process supervision
- structured audit logs
- health checks + alerting

## 7) API contract style
All relay responses should be consistent:
```json
{ "ok": true, "data": {}, "error": null }
```
Error:
```json
{ "ok": false, "data": null, "error": { "code": "...", "message": "..." } }
```

## 8) Security baseline (must keep)
- Deny-by-default for write endpoints not explicitly needed.
- Allowlist operations only.
- No secrets in client code.
- Add audit log entry for each write operation.
- Recommend Cloudflare Access before production exposure.

## 9) Acceptance criteria per milestone
### Cron module
- Can list existing jobs from host source of truth.
- Can add job and persist correctly.
- Can update/delete by id.
- UI reflects changes after action.

### Stability
- Tunnel endpoint remains reachable.
- Startup procedure documented and reproducible.

### Safety
- High-risk operations require explicit confirmation.
- Access control documented and enabled in stable mode.

## 10) Common failure branches
1. Tunnel URL expired / 530
   - Restart tunnel, update frontend API, retest health.
2. Relay alive but write fails
   - Check file permissions / schema mismatch / validation path.
3. Domain ownership blocked
   - Use quick mode temporarily; continue registrar recovery process.

## 11) Contribution protocol
- Keep commits small and atomic.
- Update docs whenever behavior changes.
- Do not silently change API contract.
- Include reproduction/verification steps in PR description.

## 12) First tasks for a new agent (copy checklist)
- [ ] Run quick start end-to-end.
- [ ] Validate cron list/add/update/delete manually.
- [ ] Add one health-check script and verify output.
- [ ] Add/refresh troubleshooting notes from real run.
- [ ] Propose next smallest production-safe increment.

## 13) Project philosophy
This project is not a hacky one-off. It is a controlled, extensible control-plane bootstrap kit.
Optimize for: reproducibility, safety defaults, clear docs, and low-friction onboarding.
