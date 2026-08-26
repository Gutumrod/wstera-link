# WSTERA Link — External Dependency Baseline

**Checked:** 2026-08-26

## Cloudflare
Current Cloudflare documentation confirms Cloudflare for SaaS/custom hostnames is available on non-Enterprise plans, with custom-hostname validation and certificate lifecycle supported. Current plan documentation shows included hostnames and metered additional hostnames; these commercial limits can change.

**Rule:** Re-verify Cloudflare for SaaS plan limits, hostname validation flow, TLS behavior and cost immediately before Phase 5 implementation and again before public launch.

## Stripe Thailand
Current Stripe support documentation confirms Thailand accounts can accept supported card payments and PromptPay in THB, among other supported currencies/payment constraints.

**V1 billing decision:** authoritative recurring SaaS subscription flow uses the payment method(s) supported by the existing Stripe adapter and verified recurring semantics. PromptPay is not promised for recurring subscription billing until the adapter/provider flow is explicitly implemented and tested.

**Rule:** Re-verify Thailand account eligibility, fees, recurring payment methods, tax/invoice obligations and webhook event model before Phase 4 production configuration.

## Supabase
Supabase provides Auth/Postgres/RLS foundation. Product-specific RLS, service-role privileges, migrations, backup policy and regional/project configuration remain WSTERA Link responsibilities.

## Dependency Policy
External vendor capability/pricing is evidence, not immutable product truth. Any vendor change that affects PRD requires an ADR before code adaptation.
