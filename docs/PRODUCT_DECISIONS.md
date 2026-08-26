# WSTERA Link — Locked Product Decisions

**Status:** LOCKED planning/build baseline  
**Date:** 2026-08-26

- Product: branded campaign link + click analytics, not generic URL shortener.
- Dashboard: `links.wstera.com`.
- Default redirect domain: `go.wstera.com`.
- Free: 5 active links, 250 tracked clicks/month, 7-day analytics, custom slug, QR, 1 destination change/link.
- Pro: ฿199/month, 500 links, 50k tracked clicks/month, 365-day analytics, campaigns/UTM/custom domain/export/unlimited destination edits.
- Business: ฿590/month, 5,000 links, 500k tracked clicks/month, 730-day analytics, Pro features + team + API/webhook.
- Quota exhaustion never disables redirect.
- Paid→Free never breaks default-domain published links solely for plan overage.
- Custom-domain downgrade has 7-day routing grace.
- Payment failure has 7-day grace.
- No promotional trial in V1 unless later ADR.
- Raw IP is not persisted as customer analytics in V1.
- No unique-visitor claim/fingerprint in V1.
- Redirect does not synchronously wait for analytics persistence.
- Supabase is authoritative data store; Cloudflare cache is not source of truth.
- Billing provider event + persisted subscription transition is authoritative for paid entitlements.
- Module Hub is read-only upstream; reused modules are copied/vendor-owned before WSTERA-specific adaptation.
- External vendor plan/capability must be re-verified at the phase that uses it.
