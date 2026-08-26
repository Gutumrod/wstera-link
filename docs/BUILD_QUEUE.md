# WSTERA Link — Build Queue

**Status:** READY after Documentation Gate

| Queue | Phase | Depends on | Primary output | Blocking gate |
|---:|---|---|---|---|
| 1 | Phase 0 Scaffold | Documentation PASS | repo/toolchain/config/CI | Build baseline PASS |
| 2 | Phase 1 Auth/Tenant/RLS | P0 | tenant schema + RLS | Cross-tenant PASS |
| 3 | Phase 2 Link/Redirect | P1 | link core + Worker | Redirect PASS |
| 4 | Phase 3 Analytics/Quota | P2 | tracking + counters | Concurrency/degradation PASS |
| 5 | Phase 4 Billing | P1 + P3 usage model | subscriptions/payment | Money Gate PASS |
| 6 | Phase 5 Paid Features | P2 + P4 | campaigns/domain/export/API/team | Entitlement/domain PASS |
| 7 | Phase 6 Hardening | P1–P5 | audit/ops/load/retention | Production readiness PASS |
| 8 | Phase 7 Beta/Launch | P6 | real beta + launch evidence | Public Launch PASS |

## Parallel Work Allowed
Marketing landing copy/assets may begin after Phase 2 UI shape is known. GTM recruitment may begin near Phase 3. Payment production onboarding and Cloudflare custom-hostname account setup may be prepared during Phases 2–3, but production integration code stays in its scheduled phase.

## First Implementation Task
Phase 0 only: initialize production repo/workspace and quality gates. Do **not** implement link business logic in Phase 0.
