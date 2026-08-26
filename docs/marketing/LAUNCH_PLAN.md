# WSTERA Link — Launch Plan

**Status:** LOCKED launch-stage baseline  
**Date:** 2026-08-26

## Launch Stages
Implementation completion is not the same as public launch. WSTERA Link progresses through evidence-based stages.

## Stage 0 — Internal Alpha
**Entry:** Phase 2 Redirect Gate PASS  
**Users:** WSTERA/internal controlled users only

Objectives:
- validate create/edit/disable/QR flows
- exercise real redirects
- confirm logging/observability

Exit:
- no blocking redirect defect
- destination update behavior understood
- smoke traffic stable

## Stage 1 — Closed Beta
**Entry:** Phase 3 Analytics/Quota Gate PASS + privacy notice ready  
**Users:** invited pilot tenants only

Target planning cohort: up to 20 tenants.

Exit criteria:
- real external traffic collected
- no known cross-tenant vulnerability
- quota behavior observed under real usage
- analytics explanations usable by pilot users
- incident/support process exercised
- blocking Beta findings closed or documented

## Stage 2 — Paid Beta
**Entry:** Phase 4 Money Gate PASS  
**Users:** selected users willing to pay

Objectives:
- prove payment → entitlement lifecycle
- prove cancellation/grace/downgrade behavior
- measure Free→Paid conversion intent
- gather support burden and billing edge cases

Exit criteria:
- successful real paid transactions
- webhook/idempotency evidence
- no entitlement forgery path
- refund/cancel/support process defined
- pricing shown equals enforced entitlements

## Stage 3 — Feature-Complete Beta
**Entry:** Phase 5 PASS

Objectives:
- custom domain
- campaigns/UTM/export
- Business team/API flows

Exit:
- custom-hostname validation lifecycle verified
- paid feature entitlements fail closed
- external dependency assumptions re-verified

## Stage 4 — Public Launch
**Entry:** Phase 6 Production Readiness PASS + all blocking Phase 7 gates PASS

Required before launch:
- production DNS/TLS
- monitoring + alerts
- backup/restore evidence
- privacy policy + terms live
- pricing/support/contact live
- security review complete
- incident drill complete
- deletion path tested
- closed and paid beta evidence accepted

## Launch Assets
- Landing page
- Pricing page
- Product demo screenshots/video
- First-link tutorial
- Custom-domain guide
- FAQ
- Privacy/Terms links
- Support/contact path
- 1+ evidence-based case study if permission exists

## Launch-Day Checklist
- [ ] Deploy approved release commit only
- [ ] Migrations applied and verified
- [ ] Health checks green
- [ ] Redirect smoke tests from multiple networks
- [ ] Signup/login test
- [ ] Free quota seed/config verified
- [ ] Payment production config verified
- [ ] Alert routing verified
- [ ] Status/support channel staffed

## Rollback Principle
Marketing launch can be paused independently. If dashboard is degraded but redirect remains healthy, protect redirects first. If redirect integrity/security is uncertain, stop new acquisition and follow Incident Runbook.

## No Vanity Launch Rule
Do not declare public launch because “code is finished.” Public launch requires evidence in `08_TEST_RELEASE_GATES.md` and this document.
