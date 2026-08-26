# WSTERA Link — System Architecture

**Status:** LOCKED pre-build baseline  
**Date:** 2026-08-26

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
```text
Checkout -> Provider
Provider webhook -> verified raw event -> idempotency/replay guard
-> normalized payment/subscription event -> subscription state transition
-> entitlement becomes authoritative -> audit event
```
The browser return URL can display pending/success UI but cannot grant entitlement.

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
