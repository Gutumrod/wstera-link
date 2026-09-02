# WSTERA Link — Test & Release Gates

**Status:** LOCKED pre-build baseline

## Every Phase
- [ ] Scope matches PRD/roadmap.
- [ ] Lint passes.
- [ ] Typecheck passes.
- [ ] Unit tests pass.
- [ ] Integration/negative tests for changed boundaries pass.
- [ ] Production build passes.
- [ ] No secrets/credentials committed.
- [ ] Evidence document records commands/results/commit.
- [ ] Independent reviewer verdict recorded.

## Security Gate
- [ ] Unauthenticated protected access denied.
- [ ] Cross-tenant select/insert/update/delete denied.
- [ ] Cross-tenant API/RPC/export denied.
- [ ] Service-role secret absent from browser bundle.
- [ ] Invalid webhook signature denied.
- [ ] Replay/duplicate provider event safe.
- [ ] LK01 billing-core credential cannot act as another product/account outside its authenticated scope.
- [ ] Reserved/unsafe slug and destination inputs rejected.

## Redirect Gate
- [ ] Active link redirects correctly.
- [ ] Missing/disabled link fails safely.
- [ ] Analytics unavailable does not block redirect.
- [ ] Dashboard unavailable does not block existing redirect.
- [ ] Destination update cache behavior bounded/tested.

## Money Gate
- [ ] Free/Pro/Business limits match `04_PRICING_ENTITLEMENTS.md`.
- [ ] Free quota exhaustion preserves redirect.
- [ ] Upgrade requires authoritative provider event.
- [ ] Card recurring failure -> 7-day recovery grace verified.
- [ ] PromptPay manual non-renewal -> reminders + 3-day post-expiry grace -> Free enforcement verified.
- [ ] PromptPay payment recovery is reconciliation-backed (provider re-fetch + expected product/account/amount/currency match), not webhook/return-page-only.
- [ ] Cancel-at-period-end verified.
- [ ] Downgrade over-limit behavior verified.
- [ ] Custom-domain grace verified.

## Production Gate
- [ ] Migrations reversible/forward-safe per runbook.
- [ ] Monitoring/alerts configured.
- [ ] Backup/restore drill completed.
- [ ] Incident runbook exercised.
- [ ] Privacy/Terms published before public users.
- [ ] Data deletion path tested.
- [ ] Production DNS/TLS verified.
- [ ] Closed Beta and Paid Beta exit criteria met.

## Verdict Values
`PASS | PASS_WITH_FOLLOWUPS | FAIL`. Public launch requires `PASS` for all blocking gates.
