# WSTERA Link — Incident Runbook

**Status:** LOCKED operational baseline  
**Date:** 2026-08-26

## Priority Order
1. Tenant/security integrity
2. Redirect correctness and availability
3. Billing/entitlement correctness
4. Data durability
5. Analytics completeness
6. Dashboard convenience

## Severity
### SEV-1
Cross-tenant exposure, malicious redirect possibility, widespread incorrect destination, credential compromise, or major redirect outage.

### SEV-2
Significant dashboard/billing/custom-domain outage while core redirect may still work; material analytics loss; repeated payment entitlement errors.

### SEV-3
Limited feature degradation, delayed analytics, isolated UI defect with workaround.

## Immediate Actions
For any incident:
- create incident timestamp/id
- identify affected component and tenant scope
- preserve logs/evidence without exposing secrets
- stop unsafe writes/feature if integrity uncertain
- communicate internally
- use status/support communication when users are impacted

## Playbook — Redirect Failure
1. Check Worker health/deployment
2. Check link-resolution datastore/cache dependency
3. Compare last known-good deployment
4. Protect against incorrect destination; fail safe if destination cannot be trusted
5. Roll back Worker if deployment-caused
6. Verify test links on default and custom domains

## Playbook — Analytics Failure
1. Confirm redirect still works
2. Inspect ingestion/queue/storage
3. Do not make redirect synchronously wait for analytics
4. Record estimated loss window
5. Recover ingestion if replay is safe; do not fabricate missing clicks

## Playbook — Supabase/DB Degradation
1. Determine whether cached resolution safely serves existing links
2. Block unsafe dashboard mutations if authoritative writes unavailable
3. Do not bypass RLS/security to restore convenience
4. Monitor vendor status/dependency

## Playbook — Billing/Webhook Failure
1. Stop new entitlement grants if authoritative verification is uncertain
2. Preserve existing valid subscription state where policy allows
3. Inspect webhook signature/idempotency/provider delivery
4. Reprocess only through idempotent authoritative path
5. Never trust browser checkout-success parameters as recovery source

## Playbook — Cross-Tenant/Security Finding
1. Treat as SEV-1
2. Disable affected endpoint/capability or fail closed
3. Preserve logs and exact access path
4. Rotate compromised secrets if relevant
5. Determine affected tenant/data scope
6. Patch + negative tests + independent review before re-enable
7. Follow legal/user notification obligations if applicable

## Playbook — Custom Domain Failure
1. Verify hostname ownership state
2. Verify TLS/certificate status
3. Verify tenant→hostname mapping
4. Prevent unknown hostname from resolving to another tenant
5. Default-domain links should remain available when policy permits

## Communication Rules
- State what is known, affected scope, workaround, and next verified update
- Do not speculate on data exposure
- Do not expose secrets/internal exploit details in public status

## Recovery Verification
- [ ] Root symptom no longer reproducible
- [ ] Security/tenant negative tests pass if relevant
- [ ] Redirect smoke tests pass
- [ ] Billing/custom-domain flows pass if relevant
- [ ] Monitoring stable
- [ ] Evidence stored

## Post-Incident Review
For SEV-1/2 document:
- timeline
- root cause
- blast radius
- detection gap
- response quality
- corrective actions
- owner/status
- whether PRD/architecture/runbook/ADR must change
