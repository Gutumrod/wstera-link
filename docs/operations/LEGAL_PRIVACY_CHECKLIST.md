# WSTERA Link — Legal & Privacy Checklist

**Status:** PRE-LAUNCH CONTROL DOCUMENT  
**Date:** 2026-08-26

## Scope
This is a product/operations checklist, not a substitute for professional legal advice. Final public terms and Thailand/other-jurisdiction obligations must be reviewed before public launch.

## Data Inventory
Document before external public launch:
- account identity data
- tenant/business profile data
- link destinations/slugs
- click timestamps
- referrer/channel/UTM
- coarse device/browser classification
- coarse geo if implemented
- billing/provider identifiers
- support/audit records

## Privacy Baseline
- [x] Raw IP not persisted in customer analytics V1
- [x] No persistent visitor fingerprint / unique visitor claim V1
- [ ] Final retention schedule implemented and documented
- [ ] Privacy policy describes analytics data and purposes
- [ ] Subprocessors/vendors documented
- [ ] User rights/contact mechanism documented
- [ ] Account/tenant deletion workflow tested

## Cookies / Client Tracking
- Inventory every cookie/local-storage/client identifier
- Distinguish essential authentication/session storage from marketing/optional tracking
- If optional tracking/consent is required by applicable law or deployment scope, implement before use
- Do not add ad pixels/marketing trackers silently

## Terms of Service Minimum Topics
- service description
- account responsibilities
- prohibited/abusive use
- link/destination content responsibility
- plan/limits
- billing/cancellation/refund policy
- suspension/termination
- availability/no-guarantee language consistent with actual commitments
- intellectual property
- liability/disclaimer reviewed for applicable law
- contact/dispute/jurisdiction terms

## Privacy Policy Minimum Topics
- controller/service identity
- categories of data
- purposes/legal basis as applicable
- retention
- sharing/subprocessors
- international transfer where applicable
- security practices at appropriate level
- rights/request process
- contact
- policy changes

## Billing / Tax / Consumer Checks
Before paid public launch:
- [ ] Confirm legal business/seller identity used for Stripe
- [ ] Confirm price presentation and currency
- [ ] Confirm tax/VAT/invoice/receipt obligations with qualified Thai accounting/legal guidance
- [ ] Confirm cancellation and refund wording
- [ ] Confirm recurring charge disclosure
- [ ] Confirm customer support/contact details

## Domain / Abuse Policy
Need policy and operational process for:
- phishing/malware links
- impersonation
- illegal content
- spam/abuse
- takedown requests
- compromised tenant accounts

Abuse response must not permit arbitrary cross-tenant access by support staff without authorization/audit.

## Data Deletion
Deletion workflow must define:
- auth/account deletion
- tenant-owned link/campaign data
- analytics deletion/retention
- billing records that must be retained for legal/accounting reasons
- append-only audit retention exceptions
- custom-domain deactivation
- backup expiry behavior

## Security/Privacy Launch Gate
- [ ] RLS/cross-tenant tests PASS
- [ ] Secrets review PASS
- [ ] Privacy policy published
- [ ] Terms published
- [ ] Data deletion tested
- [ ] Support/privacy contact active
- [ ] Vendor/subprocessor list current
- [ ] Incident notification process defined
- [ ] Legal/accounting review completed where required

## Change Rule
Any new persistent identifier, geo detail, tracking pixel, advertising integration, new payment method, or new subprocessor requires privacy/security review and document update before production use.
