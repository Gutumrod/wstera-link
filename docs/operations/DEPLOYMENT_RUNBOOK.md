# WSTERA Link — Deployment Runbook

**Status:** LOCKED operational baseline  
**Date:** 2026-08-26

## Purpose
Define safe, repeatable deployment for dashboard, Supabase schema/functions, and Cloudflare redirect runtime.

## Environments
At minimum:
- local/development
- staging/preview where practical
- production

Production secrets must be separate from development secrets.

## Deployment Order
Default order when a release changes multiple layers:
1. Verify approved commit and clean CI
2. Review migration compatibility
3. Apply backward-compatible database migration
4. Deploy server/dashboard components
5. Deploy redirect Worker only when compatible with current DB schema
6. Run smoke tests
7. Enable/verify feature exposure
8. Record evidence

If a release requires a different order, document it in the phase evidence/ADR.

## Pre-Deploy Checklist
- [ ] Phase/release gate PASS
- [ ] Approved commit/tag identified
- [ ] Lint/typecheck/tests/build green
- [ ] Secrets scan green
- [ ] Migration reviewed
- [ ] Backup/recovery point confirmed for risky migrations
- [ ] Vendor dependency changes re-verified if applicable
- [ ] Rollback path known
- [ ] Monitoring/alerts available

## Migration Rules
- Prefer additive/backward-compatible migrations
- Never assume dashboard and Worker update atomically
- RLS must be applied with tenant tables before exposing client access
- Destructive schema change requires explicit backup and rollback/forward-fix plan
- Production migration command/result recorded as evidence

## Post-Deploy Smoke Tests
- [ ] Health/readiness endpoint
- [ ] Login/authenticated dashboard
- [ ] Tenant-scoped read/write
- [ ] Create test link
- [ ] Default-domain redirect
- [ ] Analytics event path if enabled
- [ ] Quota behavior relevant to change
- [ ] Payment/webhook relevant to change
- [ ] Custom domain relevant to change

## Rollback
Rollback decision depends on layer:
- UI/server regression: roll back application when DB remains compatible
- Worker redirect regression: restore last known-good Worker immediately
- DB migration issue: prefer tested forward fix unless reversal is proven safe
- Security isolation issue: disable affected capability/fail closed; do not preserve availability over tenant security

## Redirect Priority
If dashboard/billing/analytics is degraded but authoritative link resolution is safe, preserve redirect service.

## Evidence Record
Every production deploy records:
- timestamp
- commit/tag
- operator
- migrations
- dashboard deployment ID
- Worker deployment ID
- smoke results
- incidents/follow-ups

## Secret Rules
- No production secret in repo, logs, screenshots or client bundle
- Rotate leaked credentials immediately and record incident
- Service-role credentials only in trusted server/runtime boundaries

## Emergency Change
Emergency fix still requires minimal evidence: issue, exact change, reviewer if available, deploy result, smoke test, and post-incident follow-up.
