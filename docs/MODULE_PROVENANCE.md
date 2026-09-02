# WSTERA Link — Vendored Module Provenance

**Vendored on:** 2026-08-26
**Upstream source:** `D:\AI-Workspace\projects\modules-hub`
**Upstream HEAD:** `db441ce1c5fea8ececdf56690889a0648d954f9a`
**Upstream status at copy time:** clean

## Mandatory Rule
`modules-hub` is read-only upstream. All WSTERA-specific integration/adapters/fixes happen only in the product copy. Do not edit Module Hub to make WSTERA Link work.

## 2026-09-02 Billing Disposition
The parent portfolio subsequently locked centralized `billing-core`. Therefore the vendored `subscription`, `payment`, and `webhook-receiver` copies below are **historical/reference provenance**, not the Phase 4 billing build source. Do not extend them into a product-owned Stripe state machine. Other copied modules remain local product copies subject to this provenance rule unless a later architecture decision replaces them.
## Vendored Modules
| Module | Version | Product role |
|---|---:|---|
| auth-supabase | 0.2.0 | Auth/RBAC/tenant guards |
| tenant-context | 0.3.0 | Explicit tenant context |
| subscription | 0.1.0 | Lifecycle/entitlements/limits |
| payment | 0.1.0 | Payment abstraction/Stripe adapter |
| webhook-receiver | 0.1.0 | Verification/replay protection |
| rate-limit | 0.1.0 | Request/usage enforcement core |
| audit-log | 0.1.0 | Administrative/security audit |
| config-runtime | 0.1.0 | Config validation/redaction |
| health-check | 0.2.0 | Health/readiness |
| import-export | 0.2.0 | CSV export pipeline |

Prototype reference HEAD: `bf3a9658b28461f81c324ac022e19b1188a311e9` under `references/prototype-v2/`; it is behavior reference only.
