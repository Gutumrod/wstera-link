# WSTERA Link — Product Requirements Document

**Status:** LOCKED pre-build baseline - amended by `ADR-001` and centralized billing-core reconciliation
**Date:** 2026-09-01

## 1. Product Scope
Production SaaS replacing the local Python prototype with a multi-tenant, Cloudflare-first TypeScript product.

## 2. Functional Requirements
### Identity & Tenant
- **FR-AUTH-001:** User can sign up/sign in through Supabase Auth.
- **FR-TENANT-001:** Every tenant-owned row has an authoritative tenant ID.
- **FR-TENANT-002:** Owner/Admin/Member access is resolved server-side and protected by RLS.
- **FR-TENANT-003:** Cross-tenant read/write/export/inference must fail.

### Link Core
- **FR-LINK-001:** Create generated-slug link.
- **FR-LINK-002:** Create custom slug using allowed charset/length and reserved-word rules.
- **FR-LINK-003:** Disable/enable link subject to entitlement and ownership.
- **FR-LINK-004:** Change destination without changing public short URL.
- **FR-LINK-005:** Destination must be valid `http`/`https`; unsafe schemes fail closed.
- **FR-LINK-006:** QR encodes the stable public short URL, not the current destination.
- **FR-LINK-007:** Default public domain is `go.wstera.com`.

### Redirect
- **FR-REDIRECT-001:** Valid active link redirects with 3xx to current authoritative destination.
- **FR-REDIRECT-002:** Disabled/missing/invalid link fails safely and never redirects to untrusted fallback.
- **FR-REDIRECT-003:** Analytics/billing/dashboard failure must not block a resolvable redirect.
- **FR-REDIRECT-004:** Destination changes become visible predictably after cache invalidation TTL/purge.

### Analytics
- **FR-AN-001:** Track timestamp, normalized referrer/channel, UTM fields, coarse device/browser class, tenant ID and link ID.
- **FR-AN-002:** Do not persist raw IP in analytics.
- **FR-AN-003:** V1 does not expose unique visitor claims.
- **FR-AN-004:** Bot filtering is deterministic/versioned and never blocks redirect.
- **FR-AN-005:** Dashboard supports link totals, source breakdown, recent trend and date range within plan retention.

### Quota
- **FR-Q-001:** Free = 5 active links, 250 tracked clicks/month, 7-day visible analytics.
- **FR-Q-002:** Pro = 500 active links, 50,000 tracked clicks/month, 365-day analytics.
- **FR-Q-003:** Business = 5,000 active links, 500,000 tracked clicks/month, 730-day analytics.
- **FR-Q-004:** At tracked-click limit, redirect continues; new eligible analytics events are dropped from customer analytics until reset/upgrade.
- **FR-Q-005:** Usage counters are authoritative, atomic, server-generated and concurrency-safe.

### Plans & Billing
- **FR-BILL-001:** Plan keys: `free`, `pro`, `business`.
- **FR-BILL-002:** Prices: Free ฿0, Pro ฿199/month, Business ฿590/month.
- **FR-BILL-003:** Paid entitlement is granted only after verified authoritative provider event + persisted subscription transition.
- **FR-BILL-004:** Card automatic-collection failure enters the existing 7-day recovery grace before Free enforcement. PromptPay manual non-renewal uses a 3-day post-expiry grace before Free enforcement.
- **FR-BILL-005:** Cancel-at-period-end preserves paid rights until paid-through timestamp.
- **FR-BILL-006:** Browser checkout success state is never authoritative.
- **FR-BILL-007:** WSTERA Link integrates with the portfolio centralized billing-core; it does not run a separate product-owned Stripe subscription state machine or treat vendored payment/subscription modules as authoritative billing infrastructure.
- **FR-BILL-008:** PromptPay cannot grant entitlement until billing-core has verified/re-fetched provider truth, matched product/account/amount/currency, and applied the transition idempotently; reconciliation must exist before PromptPay release.

### Paid Features
- **FR-PAID-001:** Pro/Business: campaign grouping, UTM builder, custom domain, unlimited destination edits, CSV export.
- **FR-PAID-002:** Business: API/webhook access and team access.
- **FR-DOMAIN-001:** Custom hostname requires ownership validation before activation.
- **FR-DOMAIN-002:** Paid→Free gives 7-day custom-domain routing grace; default WSTERA-domain links remain valid after grace.
- **FR-TEAM-001:** Business tenant may invite/revoke members with server-side role enforcement.

## 3. Downgrade Rules
- Existing published links never break solely because a tenant exceeds a lower plan's active-link limit.
- Over-limit tenant cannot create/reactivate until within limit or upgraded.
- Paid-only metadata remains stored but management UI/API is locked after entitlement loss.
- Analytics visibility follows current plan immediately; retention/deletion follows data policy, not UI visibility.

## 4. Non-Functional Requirements
- **NFR-REL-001:** Redirect path has no synchronous analytics write dependency.
- **NFR-SEC-001:** RLS required on every tenant-owned table before feature release.
- **NFR-SEC-002:** Secrets never ship to browser bundles or logs.
- **NFR-OBS-001:** Structured logs include request/correlation ID and sanitized error codes.
- **NFR-TEST-001:** Each phase requires unit/integration/negative security tests and evidence.
- **NFR-PERF-001:** Redirect target resolution should normally complete at edge latency appropriate to Cloudflare Worker execution; exact SLO is established from Beta measurements rather than invented pre-production.

## 5. Acceptance Rule
A requirement is complete only when implementation, automated tests, negative-path tests, migration/config evidence, and reviewer verdict all exist.
