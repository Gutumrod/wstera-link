# WSTERA Link — Documentation Index

**Pack size:** 26 documentation files  
**Documentation Gate:** PASS — READY TO QUEUE BUILD

## Source-of-Truth Order
1. `00_PRODUCT_VISION.md` — why/for whom/non-goals.
2. `01_PRD.md` — functional and non-functional product contract.
3. `02_SYSTEM_ARCHITECTURE.md` — runtime boundaries and failure behavior.
4. `03_DATA_SECURITY_TENANCY.md` — isolation/privacy/security contract.
5. `04_PRICING_ENTITLEMENTS.md` — commercial feature/limit contract.
6. `05_ANALYTICS_SPEC.md` — counting/attribution/quota definitions.
7. `06_UX_USER_FLOWS.md` — user journeys and product-state behavior.
8. `07_DEVELOPMENT_ROADMAP.md` — implementation order.
9. `08_TEST_RELEASE_GATES.md` — proof required to pass.
10. `09_EXTERNAL_DEPENDENCIES.md` — vendor assumptions and re-check points.

## Parallel Business Track
`marketing/POSITIONING_MESSAGING.md` → `marketing/GO_TO_MARKET.md` → `marketing/LAUNCH_PLAN.md` → `marketing/KPI_METRICS.md`.

## Operations
`operations/DEPLOYMENT_RUNBOOK.md`, `operations/INCIDENT_RUNBOOK.md`, `operations/LEGAL_PRIVACY_CHECKLIST.md`.

## Control Files
- `PRODUCT_DECISIONS.md` — locked decision log.
- `MODULE_PROVENANCE.md` — vendored-module source and no-upstream-edit rule.
- `MASTER_CHECKLIST.md` — project progress control.
- `BUILD_QUEUE.md` — implementation scheduling order.
- `ADR_TEMPLATE.md` — architecture decision change control.
- `DOCUMENTATION_AUDIT.md` — pre-build consistency verdict.

## Conflict Rule
Lower-numbered source-of-truth documents define intent; more specific domain documents govern their subject. If an actual conflict exists, stop implementation, write ADR, update all affected documents, then continue.
