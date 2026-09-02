# WSTERA Link — UX & User Flows

**Status:** LOCKED pre-build baseline

## Primary Activation Flow
Visitor → Sign up → Create tenant/workspace → Create first link → Copy link/QR → Receive first tracked click → View analytics.

Activation = user successfully creates first valid link. First Value = first tracked click appears in analytics.

## Create Link
1. Enter destination.
2. Optional custom slug.
3. Validate destination/slug/reserved words.
4. Check active-link entitlement.
5. Create link.
6. Show short URL + copy + QR.

## Edit Destination
Open link → edit destination → validate → check change entitlement → persist versioned mutation → invalidate route cache → audit → show success.
Free allows one lifetime destination change per link; paid allows unlimited subject to abuse controls.

## Quota Exhaustion
Dashboard warns near quota. At limit, link still redirects. Analytics UI clearly states tracking paused until reset/upgrade. Upgrade CTA must not imply links are broken.

## Upgrade
Pricing -> choose plan -> choose Card or PromptPay -> WSTERA Link requests checkout from centralized billing-core -> provider checkout/QR -> return to pending/success UI -> billing-core verifies provider event and reconciliation requirements -> product-bound entitlement snapshot updates -> UI refreshes authoritative entitlement.

## PromptPay Renewal
PromptPay user sees `paid_through` + advance reminder -> starts a fresh billing-core PromptPay checkout -> scans provider-generated QR -> UI remains pending until provider truth is verified/reconciled -> successful period extension appears exactly once. If unpaid at expiry, 3-day payment grace applies before Free enforcement; account/history are preserved.
## Cancel/Downgrade
User sees paid-through date, resulting Free limits, over-limit behavior and custom-domain grace before confirming cancellation.

## Custom Domain
Paid user → enter hostname → receive DNS/validation instructions → pending verification → verified/active → choose/use hostname for links. Errors expose actionable validation state without leaking provider secrets.

## Team (Business)
Owner/admin invites member → recipient accepts → membership created → role enforced server-side. Revoke removes access immediately; existing links remain tenant-owned.

## Delete Account/Tenant
Destructive confirmation → explain retained billing/audit obligations → queue authoritative deletion → revoke domain/routing as appropriate → completion status.

## UX Rules
- Never show paid entitlement as active before authoritative state.
- Never hide why an action is blocked: show limit, current usage and recovery action.
- Redirect failure pages must not leak destination or tenant internals.
- Mobile-first dashboard usability is required because target sellers operate heavily from phones.
