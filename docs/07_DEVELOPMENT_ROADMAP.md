# WSTERA Link — Development Roadmap

**Status:** LOCKED build sequence

Each phase follows: Objective → Scope → Tests → Evidence → Independent Gate. Do not start the next phase before the current Gate passes.

## Phase 0 — Production Scaffold
Scope: new repo/workspace, Next.js+TypeScript, Cloudflare-compatible runtime boundaries, lint/typecheck/test/build, config-runtime, health-check, CI, env examples, module provenance.
Gate: clean reproducible build/test baseline; no business feature yet.

## Phase 1 — Auth, Tenant & RLS
Scope: Supabase project schema, tenants/memberships/roles, auth helpers, tenant-context, RLS, negative cross-tenant tests.
Gate: Tenant A cannot read/write/infer Tenant B through client/API/RPC.

## Phase 2 — Link Core & Redirect Edge
Scope: link schema, slug/reserved words, safe destination validation, enable/disable, destination versioning, QR, Worker redirect, cache/version strategy.
Gate: correct redirects; safe failures; destination update propagation tested.

## Phase 3 — Analytics & Quota
Scope: event normalization, bot rules, attribution, daily aggregates, atomic usage counters, rate-limit shared adapter, Free quota behavior.
Gate: concurrency cannot bypass quota; analytics failure never blocks redirect.

## Phase 4 — Subscription & Billing
Scope: centralized billing-core client boundary, local product-bound entitlement snapshot, Card recurring checkout, PromptPay manual-renewal checkout, signed/idempotent entitlement sync, lifecycle/grace/cancel flows, reconciliation evidence and billing audit. Billing-specific vendored module copies are not the Phase 4 authority.
Gate: no unverified entitlement grant; duplicate/out-of-order events safe; Card recurring E2E passes; PromptPay cannot open until scheduled reconciliation/provider re-fetch and amount/currency/account/product matching pass.

## Phase 5 — Paid Product Features
Scope: campaigns, UTM builder, custom domains via current Cloudflare for SaaS capability, CSV export, Business API/webhooks, team access.
Gate: entitlement matrix enforced server-side; domain validation lifecycle tested.

## Phase 6 — Production Hardening
Scope: audit-log adapter, structured logs, health/readiness, abuse controls, retention jobs, backup/recovery, load/concurrency, security review.
Gate: operational/security checklist pass and failure drills completed.

## Phase 7 — Beta & Launch
Scope: production DNS, seed plans, end-to-end signup→link→track→quota→upgrade, closed beta, paid beta, launch evidence.
Gate: public-launch checklist + independent reviewer PASS.

## Change Rule
Scope-changing discoveries require an ADR and updates to PRD/architecture/affected gates before implementation continues. Product-specific changes never go upstream to Module Hub as part of this build.
