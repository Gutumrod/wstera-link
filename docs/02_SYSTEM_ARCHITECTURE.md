# WSTERA Link — System Architecture

**Status:** LOCKED pre-build baseline â€” amended by `ADR-001`
**Date:** 2026-09-01

## Runtime Topology
```text
Customer -> links.wstera.com -> Next.js Dashboard
                              -> Supabase Auth/Postgres/RLS
                              -> Subscription/Payment orchestration

Visitor -> go.wstera.com/<slug> -> Cloudflare Redirect Worker
                                -> resolve hostname+slug
                                -> redirect immediately
                                -> background analytics/usage event

Custom hostname -> Cloudflare for SaaS custom hostname -> same redirect worker/origin path
```

## Source of Truth
- Supabase Postgres: tenants, memberships, links, campaigns, domains, subscriptions, usage, aggregate analytics and audit metadata.
- Billing provider: payment transaction/provider state; normalized/persisted subscription state in Postgres controls product entitlement.
- Cloudflare edge cache: performance optimization only, never authoritative ownership/billing state.

## Component Boundaries
### Next.js Dashboard
- Authenticated UI, tenant selection, link/campaign/domain management, billing screens, exports.
- No service-role secrets in client code.

### Supabase
- Auth, relational source of truth, RLS, authoritative mutations/RPC where atomicity is required.

### Cloudflare Redirect Worker
- Hostname + slug routing, active-link validation, fast destination resolution, safe redirect.
- Emits analytics/usage work through runtime background execution after resolution.
- Must have bounded failure behavior when analytics is unavailable.

## Link Resolution
Cache key includes effective hostname + slug. Cache value contains only routing-safe fields: link ID, tenant ID, destination, active state, version/updated timestamp and expiry.
Destination mutation must invalidate/purge or advance a version so stale routes expire predictably.

## Analytics Pipeline
1. Resolve link.
2. Return redirect without waiting for persistence.
3. Background task normalizes UTM/referrer/device, filters bot, checks/consumes tracking quota atomically, persists eligible event/aggregate.
4. Analytics failure is logged/observable but does not change a successful redirect response.

## Billing Flow
V1 uses the portfolio **centralized billing-core** with one entitlement contract and two Stripe payment rails. WSTERA Link does not own a separate Stripe subscription orchestrator.

```text
WSTERA Link control plane
        |
        | per-product authenticated billing-core call
        v
Central billing-core / thin orchestrator
        |
        +--> Card checkout -> Stripe Subscription recurring rail
        |
        +--> PromptPay checkout -> fresh QR / manual renewal rail
                          |
                          v
         verified provider event + durable idempotency/outbox
                          |
               scheduled reconciliation / re-fetch
                          |
          normalized subscription/payment transition
                          |
             LK01 entitlement snapshot sync
```

- Card may renew automatically through Stripe Billing.
- PromptPay is user-initiated for each renewal period and must never be described as auto-renew.
- PromptPay non-renewal receives the owner-approved reminder flow and a 3-day post-expiry grace before Free enforcement for LK01.
- A PromptPay renewal extends the purchased period exactly once. Duplicate/replayed/out-of-order events cannot extend entitlement twice.
- **Reconciliation is mandatory before PromptPay activation:** provider truth is re-fetched/polled and product/account/amount/currency are matched before entitlement mutation.
- The browser return URL can display pending/success UI but cannot grant entitlement.
- The redirect hot path never calls billing-core synchronously. LK01 uses a bounded local entitlement snapshot for control-plane feature enforcement; redirect availability remains independent of billing availability.
- The billing-specific vendored `payment` / `subscription` / `webhook-receiver` copies are historical/reference material after the centralized billing-core decision and are not the Phase 4 build source.
## Custom Domains
Use Cloudflare for SaaS exact custom hostnames with ownership/certificate validation. V1 supports customer hostnames/subdomains; apex behavior is not promised unless the chosen Cloudflare capability supports the customer's DNS case.
Custom-domain integration belongs to Phase 5 and must be re-verified against current Cloudflare limits before implementation.

## Failure Matrix
| Dependency failure | Required behavior |
|---|---|
| Analytics DB/write failure | Redirect continues; event may be dropped/retried per bounded policy |
| Dashboard unavailable | Existing redirects continue |
| Billing provider unavailable | Existing authoritative entitlement remains; no unverified upgrade |
| Subscription lookup degraded | Management actions fail closed; redirect uses link state, not live billing call |
| Supabase authoritative link lookup unavailable and cache miss | Fail safely; never guess destination |
| Cache stale after destination update | Bounded by version/purge/TTL policy and monitored |

## Vendor Module Boundary
Vendored modules live under `vendor/modules`. WSTERA-specific adapters/orchestration live in product-owned integration code. Upstream `modules-hub` is never modified to make this product work.
