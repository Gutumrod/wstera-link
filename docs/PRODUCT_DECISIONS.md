# WSTERA Link — Locked Product Decisions

**Status:** LOCKED planning/build baseline
**Date:** 2026-08-26; billing amendment reconciled 2026-09-02

- Product: branded campaign link + click analytics, not generic URL shortener.
- Dashboard: `links.wstera.com`.
- Default redirect domain: `go.wstera.com`.
- Free: 5 active links, 250 tracked clicks/month, 7-day analytics, custom slug, QR, 1 destination change/link.
- Pro: ฿199/month, 500 links, 50k tracked clicks/month, 365-day analytics, campaigns/UTM/custom domain/export/unlimited destination edits.
- Business: ฿590/month, 5,000 links, 500k tracked clicks/month, 730-day analytics, Pro features + team + API/webhook.
- Quota exhaustion never disables redirect.
- Paid→Free never breaks default-domain published links solely for plan overage.
- Custom-domain downgrade has 7-day routing grace.
- Card automatic-payment failure has 7-day recovery grace.
- PromptPay is manual/non-auto-renew; LK01 unpaid PromptPay renewal has a 3-day post-expiry grace before Free enforcement, while account/history are preserved.
- Custom-domain routing grace remains a separate 7-day downgrade policy after transition to Free.
- No promotional trial in V1 unless later ADR.
- Raw IP is not persisted as customer analytics in V1.
- No unique-visitor claim/fingerprint in V1.
- Redirect does not synchronously wait for analytics persistence.
- Supabase is authoritative data store; Cloudflare cache is not source of truth.
- Billing provider event + persisted subscription transition is authoritative for paid entitlements.
- Centralized billing-core is the payment/subscription orchestration authority for LK01; Card is recurring, PromptPay is manual renewal, and reconciliation is mandatory before PromptPay activation.
- Module Hub is read-only upstream; reused modules are copied/vendor-owned before WSTERA-specific adaptation.
- External vendor plan/capability must be re-verified at the phase that uses it.
