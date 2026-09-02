# WSTERA Link — External Dependency Baseline

**Checked:** 2026-08-26; billing decision reconciled 2026-09-02

## Cloudflare
Current Cloudflare documentation confirms Cloudflare for SaaS/custom hostnames is available on non-Enterprise plans, with custom-hostname validation and certificate lifecycle supported. Current plan documentation shows included hostnames and metered additional hostnames; these commercial limits can change.

**Rule:** Re-verify Cloudflare for SaaS plan limits, hostname validation flow, TLS behavior and cost immediately before Phase 5 implementation and again before public launch.

## Stripe Thailand
Current Stripe support documentation confirms Thailand accounts can accept supported card payments and PromptPay in THB, among other supported currencies/payment constraints.

**V1 billing decision:** centralized billing-core uses Stripe Card/Subscription as the automatic recurring rail and PromptPay as a manual, user-initiated renewal rail. PromptPay is explicitly **not** auto-renew. Before Phase 4 implementation it remains a hard preflight to verify the selected Stripe account is Thailand-based/PromptPay-eligible, pin the Stripe API version, and prove both test-mode flows. Reconciliation/provider re-fetch must exist before PromptPay can pass the Money Gate.

**Rule:** Re-verify Thailand account eligibility, fees, recurring payment methods, tax/invoice obligations and webhook event model before Phase 4 production configuration.

## Supabase
Supabase provides Auth/Postgres/RLS foundation. Product-specific RLS, service-role privileges, migrations, backup policy and regional/project configuration remain WSTERA Link responsibilities.

## Dependency Policy
External vendor capability/pricing is evidence, not immutable product truth. Any vendor change that affects PRD requires an ADR before code adaptation.
