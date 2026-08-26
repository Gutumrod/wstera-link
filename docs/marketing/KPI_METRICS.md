# WSTERA Link — KPI & Metrics Framework

**Status:** LOCKED measurement baseline  
**Date:** 2026-08-26

## Measurement Principle
Product metrics must represent real product value, not vanity traffic.

## North-Star Metric
**Active tracked links receiving real clicks**

Operational definition: count of enabled links that receive at least one accepted `click.tracked` during the selected reporting period.

## Funnel Metrics
### Acquisition
- Landing visitors
- Signup started
- Signup completed

### Activation
- Tenant created
- First link created
- First real tracked click received
- Activated tenant rate

Activated tenant = created at least one link + received at least one accepted tracked click.

### Engagement
- Weekly Active Tenant (WAT)
- Active tracked links per tenant
- Tracked clicks per active tenant
- Tenants returning to analytics dashboard
- Campaign usage among entitled tenants

### Monetization
- Free→Paid conversion
- Pro subscribers
- Business subscribers
- MRR
- ARPA
- Upgrade/downgrade count
- Payment failure recovery rate

### Retention
- Tenant retention by signup cohort
- Paid logo retention
- Revenue retention
- Cancellation rate
- Voluntary vs payment-failure churn

## Product-Quality Metrics
- Redirect success rate
- Redirect error rate by category
- Analytics ingestion acceptance/drop rate
- Bot-filtered rate
- Quota-dropped event count
- Cache miss/error rate
- Custom-domain validation success/failure
- Support tickets per 100 active tenants

## Guardrail Metrics
Growth must not hide:
- security incidents
- cross-tenant access findings
- redirect latency/error degradation
- billing entitlement errors
- privacy/deletion failures

## Analytics Caveat
WSTERA Link V1 does not claim unique visitors. Do not derive MAU/WAU from persistent visitor identity. “Weekly Active Tenant” is tenant activity, not unique consumer traffic.

## KPI Review Cadence
- Internal Alpha: reliability/debug metrics
- Closed Beta: activation + engagement + reliability
- Paid Beta: add conversion/billing/churn signals
- Public: weekly product KPI review + monthly business review

## Decision Threshold Rule
Before enough data exists, targets are hypotheses rather than promises. Record target changes in a decision log/ADR when they affect roadmap, pricing, or launch gates.

## Dashboard Minimum
Internal operator dashboard should expose:
- activated tenants
- active tracked links
- accepted tracked clicks
- quota drops
- redirect errors
- paid tenants/MRR when billing is live
- cancellations/payment failures
- current incident/health status
