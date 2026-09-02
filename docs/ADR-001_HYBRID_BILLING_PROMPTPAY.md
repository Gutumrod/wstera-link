# ADR-001 - Hybrid Billing for Thai Users

**Status:** Accepted - reconciled with centralized billing-core on 2026-09-02
**Original decision:** 2026-09-01
**Current authority relationship:** this ADR defines LK01 payment-rail/product behavior; parent `docs/platform/BILLING_CORE_PLAN.md` defines shared billing implementation.

## Context
WSTERA Link targets Thai online sellers, creators, affiliate operators and small businesses. A card-only recurring flow creates avoidable friction for users who primarily pay by PromptPay QR.

The 2026-09-01 WSTERA Payment Council and owner decisions lock one shared architecture: centralized billing-core remains the only common billing service; Stripe Card/Subscription is the automatic recurring rail; PromptPay is a manual, user-initiated rail and must not be represented as auto-renew. PromptPay must inherit the same money-correctness, idempotency, audit and reconciliation requirements as card payments.

## Decision
- V1 offers Card and PromptPay where the selected Stripe Thailand account and current provider capability pass Phase 0 preflight.
- Card is the automatic recurring path through Stripe Billing/Subscription.
- PromptPay is the manual prepaid renewal path: the user initiates each renewal by creating/scanning a fresh provider-generated QR.
- PromptPay must never be described as automatic recurring billing.
- Both rails purchase the same product entitlement for a selected plan; payment method does not create a parallel plan/state machine.
- WSTERA Link does **not** run a separate product-owned Stripe orchestrator. It calls centralized billing-core using a product-bound server credential and receives/synchronizes a bounded local entitlement snapshot.
- Browser return state cannot grant entitlement.
- Every successful paid period is applied exactly once. Duplicate, replayed and out-of-order events cannot double-extend or regress entitlement.
- **Reconciliation is mandatory before PromptPay activation:** billing-core re-fetches/polls provider truth and verifies expected product/account/amount/currency before a payment can grant/restore entitlement.
- Card automatic-collection failure follows LK01's existing 7-day recovery grace.
- PromptPay non-renewal is a different condition: notify before expiry, preserve account/history, allow a 3-day post-expiry payment grace, then enforce Free if no verified renewal exists.
- Custom-domain routing grace is independent: after a tenant actually transitions to Free, the existing 7-day custom-domain routing grace applies before custom-hostname routing is disabled.
- Refund handling in the current internal-first WSTERA phase is support-ticket/manual-operator handling; no automated refund subsystem is part of LK01 Phase 4.

## Provider Preflight
Before implementation evidence can rely on PromptPay:
1. verify the selected Stripe account is Thailand-based and PromptPay-eligible;
2. exercise PromptPay in Stripe test mode;
3. pin an explicit Stripe API version;
4. prove a basic Card Subscription test flow;
5. prove a basic PromptPay test flow;
6. record current provider limitations/fees/compliance dependencies without hard-coding commercial assumptions into source.

## Architecture Consequences
- Phase 4 integrates LK01 with centralized billing-core instead of extending the billing-specific vendored module copies.
- Public redirect requests never call billing-core synchronously.
- LK01's local entitlement snapshot is bounded/stale-aware and used for product authorization/control-plane features; provider money truth and normalized billing transitions remain outside the redirect hot path.
- Scheduled reconciliation/pending-payment recovery must exist before PromptPay is released.
- Billing-core's event ledger/outbox, product binding, retry, audit-redaction and out-of-order rules apply equally to both rails.

## Alternatives Considered
- **Card-only recurring:** rejected because it excludes an important Thai payment behavior.
- **PromptPay-only:** rejected because it removes automatic renewal for card users.
- **Separate LK01 billing core / product-owned Stripe orchestrator:** rejected because the portfolio already has an owner-locked centralized billing-core.
- **Manual bank transfer/slip review:** not the V1 payment rail because it weakens automated provider verification/reconciliation compared with provider-confirmed PromptPay.

## Money Gate
Before Phase 4 can PASS, tests/evidence must prove:
- Card recurring checkout/renewal and 7-day recovery grace;
- PromptPay manual checkout/renewal and 3-day post-expiry grace;
- verified signatures/event intake and atomic idempotency;
- duplicate/replay/out-of-order safety;
- reconciliation/provider re-fetch + product/account/amount/currency matching;
- no browser authority;
- product-bound billing-core credential isolation;
- local entitlement snapshot behavior during billing-core/provider outage;
- redirect hot-path independence.

## Documents Affected
- [x] PRD
- [x] Architecture
- [x] Security/Tenancy
- [x] Pricing/Entitlements
- [x] UX Flow
- [x] Roadmap/Gates
- [x] External Dependencies
- [x] Product Decisions
- [x] Module Provenance
- [x] Documentation Audit addendum

## Change Rule
If Stripe/PromptPay capabilities or the parent billing-core contract changes materially, re-open this ADR and update every checked document before implementation continues.
