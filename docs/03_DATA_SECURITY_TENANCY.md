# WSTERA Link — Data, Security & Tenancy

**Status:** LOCKED pre-build baseline

## Tenant Model
- Tenant is the billing/data boundary.
- Membership roles V1: `owner`, `admin`, `member`.
- Owner: full tenant management + billing + members.
- Admin: link/campaign/domain operational management; no ownership transfer.
- Member: day-to-day link/campaign use according to explicit permissions.
- Unknown role/permission fails closed.

## RLS Rules
- Every tenant-owned table includes `tenant_id` and RLS before production use.
- Client-provided `tenant_id` is never trusted without authenticated membership validation.
- Service-role operations are server-only and narrowly scoped.
- Cross-tenant negative tests cover direct select, insert, update, delete, RPC, export, guessed IDs and API routes.

## Billing Trust Boundary
- WSTERA Link never holds billing-core database credentials or Stripe secret keys.
- LK01 uses a product-bound server credential to call centralized billing-core control-plane routes; a credential for LK01 cannot select another product identity.
- Billing-core/provider events are not sufficient merely because they arrived: signature, replay/idempotency and provider reconciliation rules must pass before local entitlement snapshot changes.
- Browser return state, client-supplied account/product IDs and redirect-query data cannot grant entitlement.
- Billing-core is never called synchronously from the public redirect hot path.
## Sensitive Data
- Secrets: provider keys, service-role keys, webhook secrets, signing secrets and domain-provider credentials.
- Secrets come from runtime env/secret store, never source code, client bundles, audit payloads or raw logs.
- Config logging uses redaction.

## Analytics Privacy V1
- Raw client IP may be available transiently at the edge for routing/security but is **not persisted in analytics**.
- Coarse country/region may be derived transiently and stored if provided by trusted edge metadata.
- No stable hashed visitor ID, fingerprint, cross-site identity graph, or cross-device tracking in V1.
- User-Agent is normalized to coarse browser/device class; raw UA retention should be avoided unless short-lived operational debugging requires it.
- Referrer storage is normalized to source/hostname and avoids arbitrary query-string retention.

## Abuse/Ratelimit Privacy
Operational anti-abuse may derive a rotating pseudonymous key from request network data. It must not be exposed as customer analytics and should have short retention (target <=24h) unless an incident requires documented extension.

## Retention
- Free visible analytics: 7 days.
- Pro visible analytics: 365 days.
- Business visible analytics: 730 days.
- Audit/security records follow operational/legal retention defined before production launch.
- Hidden data is not automatically promised forever; retention jobs must follow documented plan/privacy policy.

## Account/Data Deletion
- Tenant owner can request account deletion through supported product flow/support process.
- Deletion job must remove tenant business data and custom-domain configuration, subject to legally/operationally required billing/audit retention.
- Authentication account deletion and tenant deletion are separate operations when a user belongs to multiple tenants.
- Backup expiration means deletion from backups may be delayed until backup rotation; this must be disclosed.

## Audit Required Actions
Destination changes, link enable/disable, domain create/verify/remove, member/role changes, billing/subscription transitions, admin quota overrides and destructive data operations.

## Security Gate
No phase handling tenant data can pass without demonstrated RLS and negative cross-tenant tests. No billing phase can pass without verified signature + replay/idempotency tests.
