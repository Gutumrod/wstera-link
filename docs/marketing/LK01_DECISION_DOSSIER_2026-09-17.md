# LK01 Decision Dossier — 2026-09-17

**Product:** WSTERA Link (LK01)  
**Document type:** Decision-support evidence pack  
**Status:** DESK RESEARCH COMPLETE / PRIMARY EVIDENCE OPEN / NO NEW PRODUCT DECISION AUTHORIZED  
**Research branch:** `docs/lk01-market-validation-20260917`  
**Canonical product baseline reviewed:** `docs/hybrid-billing-promptpay` @ `ae7c4747473763e942d48807e1ac9576f42bc9bb`  
**Review date:** 2026-09-17

> This document does not replace Product Vision, PRD, Product Decisions, pricing, positioning, or Owner decisions. It exists to place the currently available evidence, contradictions, unknowns, and structural product options in one place before the Owner makes any new decision.

---

## 1. Decision rule for this dossier

No new positioning, ICP, payer, price, packaging, standalone/module status, roadmap scope, or go-to-market thesis is locked by this document.

Every statement is classified as one of:

- **VERIFIED — PRODUCT:** supported by LK01 repository/implementation evidence.
- **VERIFIED — MARKET:** supported by current first-party or authoritative external evidence.
- **ANECDOTAL:** community/user reports that are useful signals but not representative proof.
- **REASONED INFERENCE:** follows from verified facts but has not itself been directly validated with LK01 users.
- **UNKNOWN / PRIMARY EVIDENCE REQUIRED:** cannot be settled by desk research.

The dossier is intentionally allowed to end with unresolved choices.

---

## 2. Canonical product state

### VERIFIED — PRODUCT

The current locked planning model describes LK01 as a **branded campaign-link and click-analytics SaaS**, not a generic URL shortener.

Current planned segments include:

1. Thai online sellers / social-commerce operators.
2. Creators and affiliate operators.
3. Small businesses using social links / QR.
4. Agencies and social admins.

The existing product promise combines four jobs:

- keep one public link stable while changing its destination;
- create QR assets around that stable public link;
- observe click/source/campaign analytics;
- add branded/custom domains and operational paid features.

The repository contains a detailed production PRD but no production LK01 application yet. The current executable code is a reference FastAPI/SQLite prototype and does not implement the full contract.

### Current historical package baseline — not final public pricing

| Plan | Historical planning price | Main planning limits/features |
|---|---:|---|
| Free | ฿0 | 5 active links, 250 tracked clicks/period, 7-day analytics, custom slug, QR, one destination change/link |
| Pro | ฿199/mo | 500 links, 50k tracked clicks, 365-day analytics, campaigns/UTM/custom domain/export/unlimited destination changes |
| Business | ฿590/mo | 5,000 links, 500k tracked clicks, 730-day analytics, Pro + team + API/webhook |

A newer local Owner-authored Build-to-Sell execution brief exists in the working tree but is currently **untracked** and was not modified by this research. It explicitly says that historical ฿199/฿590 pricing is not automatically approved public pricing and that paid launch requires real WTP/package evidence.

That same brief authorizes `LK-SR-01` production scaffold work and does not constitute proof of product-market fit.

---

## 3. Existing GTM and measurement contract

### VERIFIED — PRODUCT

The existing GTM already defines the purpose of early users as proving:

- activation;
- repeat usage;
- willingness to pay;
- reasons to pay / not pay;
- reliability under real traffic.

The planned acquisition sequence is internal dogfood → friendly/pilot businesses → seller/creator communities → content/SEO → referral/agency.

The launch plan already separates Internal Alpha, Closed Beta, Paid Beta, Feature-Complete Beta, and Public Launch. It explicitly says finished code is not sufficient for public launch.

The KPI framework tracks activation, weekly active tenants, returning analytics users, free→paid conversion, MRR/ARPA, retention/churn and product-quality guardrails. It also states that thresholds before enough data exists are hypotheses, not promises.

### Implication

The repository architecture already supports evidence-based iteration. The missing layer is primary market evidence, not another theoretical KPI framework.

---

## 4. Thailand opportunity baseline — market context, not TAM

### VERIFIED — MARKET

Current public data shows a large digitally active business/customer environment in Thailand:

- SME Big Data / OSMEP reports roughly **3.28 million SMEs in 2025** and about 13.6 million SME employment positions.
- DataReportal's Digital 2026 Thailand report estimates **67.8 million internet users** at the end of 2025 and **56.6 million social-media user identities** in October 2025. Social-media identities are not necessarily unique people.
- ETDA historical e-commerce research shows e-marketplaces, owned websites/apps and social commerce are all major Thai sales channels; its 2022/2023 dataset is useful as structural evidence but should not be presented as a 2026 LK01 TAM.
- ETDA's SME digital-maturity work indicates many Thai SMEs use digital tools without strong integration across workflows.

### What this evidence proves

Thailand has a large digital-commerce and social-commerce base.

### What this evidence does NOT prove

It does not tell us:

- how many businesses need link-management software;
- how many use multiple channels often enough to have a recurring pain;
- how many would switch from free/native tools;
- how many would pay monthly;
- how many require custom domains, APIs or team workflows.

Therefore no defensible LK01 TAM/SAM/SOM should be derived by multiplying SME counts by a guessed conversion percentage.

---

## 5. Global competitor reality

### VERIFIED — MARKET

| Product | Current relevant evidence | Meaning for LK01 |
|---|---|---|
| Bitly | Free around 5 links/month; paid plans add larger link limits, UTM tooling, redirects, branded/custom domains and deeper campaign analytics. | Category leader already owns the basic mental model. |
| Rebrandly | Free and low-cost plans include branded-link management; current Free includes limited links plus custom/free branded-domain options, while higher plans add destination edits, routing, workspaces and team capabilities. | Branding + link operations are mature commodities. |
| Short.io | Current Free includes 5 custom domains, 1,000 branded links total and 50,000 tracked clicks/month; paid tiers start at low USD prices. | Planned LK01 Free/Pro limits cannot be defended by quota/custom-domain value alone. |
| Dub | Free includes custom domains, links, API, UTM templates, QR and analytics; higher tiers extend into conversion tracking, customer insights, experiments and event webhooks. | Modern category competition is moving from click analytics toward conversion/partner infrastructure. |
| Beacons | Link-in-bio, analytics, affiliate links, store/email and creator tools are bundled into one creator platform; custom-domain capability appears in paid creator tiers. | Creators may prefer a broader creator operating system rather than a dedicated link tool. |

### VERIFIED conclusion from category evidence

The combination `short link + QR + analytics + editable destination + custom domain + low price` is widely available and is not, by itself, a unique product position.

---

## 6. Thailand/local competitor reality

### VERIFIED — MARKET

| Product | Current first-party evidence | Relevant overlap |
|---|---|---|
| URLkub | Free plan plus paid Plus around ฿199/mo and Pro around ฿399/mo; paid functionality includes more links/QR, destination edits, UTM and richer analytics. | Directly overlaps the historical LK01 Pro price and basic workflow. |
| SHORTURL.IN.TH | Pro around ฿99/mo and Business around ฿299/mo; vendor lists branded domains, campaigns/channels, deep linking, targeting, A/B/rotator, pixels, API and import/export. | Competes on very low Thai pricing and a broad feature list. |
| WaanKit | Dynamic QR/short links, analytics and paid marketing features; Starter around ฿290 monthly or lower annual-equivalent pricing; higher tiers add teams, tracking integrations and enterprise/custom-domain/on-premise options. | Strong overlap for dynamic QR/offline marketing and Thai business operations. |
| nConnect ShortURL | Cloud ฿2,990/year or self-hosting ฿5,950 one-time; custom domain, analytics/referrer reporting, UTM builder, QR and multiple users. | Introduces a different buying argument: ownership/self-hosting and avoiding recurring SaaS subscription. |

### VERIFIED conclusion from local evidence

The following cannot be assumed to differentiate LK01 on their own:

- Thai language;
- Thai-oriented pricing;
- PromptPay;
- QR;
- custom domains;
- basic click analytics;
- editable destination;
- UTM builder.

PromptPay can reduce payment friction. It is not evidence of a product-level reason to switch.

---

## 7. Native platform substitution — affiliate use case

### Shopee — VERIFIED / PARTLY VERIFIED

Shopee Affiliate documentation exposes native reporting around clicks, orders and revenue/commission-related activity. Shopee's `Sub ID` mechanism is designed to let affiliates distinguish promoted links and inspect click/order outcomes by identifier.

This means the broad pain statement that affiliate operators become unable to measure anything after sending traffic to Shopee is inaccurate.

Shopee also exposes an Affiliate Open API landing surface, but this desk research did **not** verify detailed Thailand scopes, approval rules, rate limits, production eligibility or whether LK01 could obtain the exact data required for a commercial cross-platform product.

**Shopee API integration feasibility remains OPEN.**

### TikTok Shop — VERIFIED — MARKET

TikTok Shop's creator/affiliate reporting includes downstream commercial metrics such as GMV/items sold and traffic-source distributions for affiliate links.

TikTok Shop also has Affiliate APIs for development partners. Current documentation includes creator-order access and 2026 offline/export-style affiliate analytics endpoints.

However, Affiliate API access is not simply public-by-default: current partner documentation says affiliate API access is inactive by default and partners/ISVs must apply and receive approval through TikTok Shop partner/account-management processes.

### Consequence

Native marketplace/platform reporting can be deeper than LK01 V1 redirect analytics because the platform can observe checkout/order/GMV events that a redirect layer cannot infer by itself.

A cross-platform product may still have value, but it would have to add value **between** native systems — normalization, workflow, reconciliation, reporting, campaign operations or governance — rather than pretending to replace platform-authoritative conversion truth.

---

## 8. Attribution truth and technical limits

### VERIFIED — PRODUCT

LK01's own analytics specification already defines source attribution precedence as:

1. explicit UTM source;
2. normalized referrer source/hostname;
3. `Direct / None`.

Unknown sources are not supposed to be guessed.

### VERIFIED — WEB STANDARD

HTTP `Referrer-Policy` can reduce or completely omit the `Referer` header. `no-referrer` sends none; `same-origin` sends none cross-origin; the common default `strict-origin-when-cross-origin` generally exposes only the origin on eligible cross-origin navigation.

Google Analytics documentation recommends explicit campaign parameters and a distinct `utm_source` per platform/channel when reliable campaign/source reporting is required.

### Consequence

The current marketing headline **“ลิงก์เดียว รู้ว่าลูกค้ามาจากไหน”** is broader than the deterministic technical guarantee.

If one identical untagged LK01 URL is posted to multiple channels and the browser/platform supplies no useful referrer, LK01 cannot manufacture the originating channel with certainty.

Any future positioning must distinguish:

- click/redirect facts LK01 directly observes;
- explicit campaign/source tags LK01 controls;
- native platform conversion/order data;
- inferred or unavailable information.

---

## 9. Buyer, user, payer and gatekeeper map

Desk research identifies multiple plausible roles but does not prove which one should be LK01's economic buyer.

| Role | Possible job | Possible payer? | Evidence status |
|---|---|---|---|
| Individual creator / affiliate | create links, distribute campaigns, understand performance | Possible | Segment exists; WTP unknown; free native tools are strong substitutes |
| SME/store owner | control destinations/QR/brand links, compare channels | Possible | Segment exists; recurring pain and budget authority not proven |
| In-house marketer/social admin | campaign operations and reporting | Possible via employer | Workflow plausible; purchasing process unknown |
| Small agency | manage multiple client campaigns/assets/reports | Plausible | Competitor team/workspace pricing supports category demand; LK01 buyer evidence absent |
| MCN / affiliate manager | coordinate creators, offers, links, outcomes and reporting | Plausible | Platform ecosystems explicitly include MCNs/partners; Thai LK01 WTP unproven |
| TikTok Shop Partner / ISV | build partner tools using approved Affiliate APIs | Business model possible | Requires platform approval/access; not guaranteed |
| Enterprise/offline marketing team | dynamic QR, branded domains, governance | Possible | Established local competitors already serve this workflow |

### Important structural distinction

For a cross-platform product, four roles may be different:

- **User:** person operating campaigns.
- **Economic buyer:** person/company approving subscription spend.
- **Data authorizer:** owner of the marketplace/creator/seller account granting OAuth/API access.
- **Platform gatekeeper:** Shopee/TikTok or another platform controlling API eligibility.

A product can have strong end-user interest and still fail commercially if the economic buyer or platform gatekeeper does not cooperate.

### UNKNOWN / PRIMARY EVIDENCE REQUIRED

The current repo does not establish which role owns the strongest recurring pain, budget and purchasing authority.

---

## 10. Willingness-to-pay evidence

### What desk research shows

Users in the broader category pay for combinations of:

- custom-domain/brand control;
- higher traffic/volume;
- destination/routing controls;
- teams/workspaces/governance;
- client reporting;
- export/API/webhook automation;
- conversion or revenue attribution;
- security/reliability/compliance;
- data ownership/self-hosting;
- complex multi-network campaign operations.

Community anecdotes also show both sides of the market:

- some users want better analytics without expensive enterprise pricing;
- some high-volume technical users build their own stack to avoid SaaS cost;
- dynamic QR users frequently look for free/cheap alternatives when editing is paywalled;
- affiliate operators managing many programs often fall back to spreadsheets or specialist tracking/reporting products.

### What desk research does NOT prove

It does not prove that LK01's intended Thai buyer will pay:

- ฿199;
- ฿590;
- any recurring subscription at all;
- specifically for click analytics;
- specifically for cross-platform normalization;
- specifically for custom domain or QR.

No interview answer such as “น่าสนใจ” should be treated as WTP evidence.

### Primary proof standard

Strong WTP evidence should involve a real cost-bearing action, e.g. paid beta, deposit, approved purchase, signed pilot with a price, or renewal after a real billing period.

---

## 11. Pricing benchmark and payment economics

### VERIFIED — MARKET

Current benchmarks span several models:

- free-heavy global SaaS;
- low-cost monthly Thai SaaS from roughly ฿99 upward;
- mid-tier Thai dynamic-QR/marketing subscriptions;
- annual hosted pricing;
- one-time/self-hosted licensing;
- global creator suites bundling links into broader subscriptions.

Therefore monthly SaaS is not the only viable pricing architecture in this category.

### Current payment fees — Thailand

Stripe's current Thailand standard pricing lists:

- domestic cards: **3.65% + ฿10** per successful transaction;
- international cards: **4.75% + ฿10**;
- PromptPay: **1.65%** per successful transfer;
- no standard setup/monthly fee for basic payments.

### Illustration only — historical LK01 prices

If a hypothetical ฿199 payment used a domestic card, payment cost is about ฿17.26 and net before all other costs is about ฿181.74. PromptPay cost is about ฿3.28 and net about ฿195.72.

At hypothetical ฿590, domestic-card cost is about ฿31.54 and net about ฿558.47; PromptPay cost is about ฿9.74 and net about ฿580.27.

These are **not pricing recommendations** and exclude VAT/tax, refunds/disputes, infrastructure, support, acquisition, abuse operations and labor.

---

## 12. Infrastructure cost floor and scaling shape

### VERIFIED — MARKET

Current published vendor rates include:

- Cloudflare Workers Paid: $5/month minimum, 10 million requests/month included, then $0.30 per additional million requests; CPU is separately metered beyond included capacity.
- Cloudflare for SaaS: available on non-Enterprise plans; current plans include 100 custom hostnames and charge $0.10 for additional hostnames up to documented non-Enterprise limits.
- Supabase Pro: from $25/month, including one project, 100k MAU, 8 GB disk and 250 GB egress before overage rates.

Using a working 2026-09-17 exchange rate around ฿33.36/USD, a dedicated Cloudflare Workers $5 + Supabase Pro $25 baseline is roughly **฿1,001/month** before other services.

### Important qualification

WSTERA may share infrastructure, billing, observability or operational resources across products. Therefore ฿1,001/month is an illustrative dedicated-product floor, **not verified incremental LK01 cost**.

At historical ฿199/฿590 price points, raw infrastructure is unlikely to be the only or even largest business-model risk. CAC, support burden, abuse response, refunds, API partnership/access costs and founder/operator time may dominate at low ARPA.

### UNKNOWN

No reliable CAC, support-cost, API-partnership cost, chargeback rate, churn or LTV data exists for LK01 yet, so a meaningful LTV:CAC model cannot currently be calculated.

---

## 13. Acquisition and distribution

### VERIFIED — PRODUCT

Existing LK01 GTM proposes:

1. internal dogfood;
2. friendly/pilot businesses;
3. seller/creator communities;
4. content/SEO;
5. referral/agency after workflow maturity.

### VERIFIED — MARKET

TikTok Shop partner documentation explicitly presents an ecosystem for approved development partners/ISVs and says integrated applications can receive distribution/exposure through the partner/app environment. This is a possible distribution route only if the required partner/API access is approved.

Shopee has affiliate/MCN structures and an Affiliate Open API surface, but this research did not establish an equivalent validated distribution path for LK01.

### UNKNOWN

No LK01 evidence exists yet for:

- visitor→signup rate;
- signup→activation rate;
- acquisition cost by channel;
- community/content conversion;
- referral rate;
- agency channel economics;
- sales-cycle length;
- self-serve vs assisted-sales requirement.

SEO/content can be part of acquisition, but current global/local competition makes it unsafe to assume cheap organic acquisition.

---

## 14. Retention / recurring-value analysis

### VERIFIED — PRODUCT

LK01 intentionally keeps default-domain links working after quota exhaustion/downgrade rather than breaking published customer assets.

### VERIFIED — MARKET

Competitors also commonly preserve core links while restricting analytics/features or paid operational capabilities.

### REASONED INFERENCE

Because the base redirect itself should continue working, recurring retention cannot depend on holding a customer's published links hostage.

Recurring subscription value would need to come from repeated operational jobs such as:

- active campaign creation/changes;
- analytics/report review;
- team governance;
- client reporting;
- API/webhook automation;
- custom-domain operations;
- campaign/source normalization;
- marketplace reconciliation.

A user who creates one permanent link or QR and rarely revisits it is structurally less attractive for monthly retention than a user operating campaigns every week.

### UNKNOWN

No LK01 cohort has yet demonstrated repeat usage, paid retention or renewal.

---

## 15. Cross-platform / affiliate operations feasibility

This is a **hypothesis area**, not a new positioning decision.

### Potential value loop

A cross-platform operations product could theoretically:

1. define campaign/source naming centrally;
2. issue controlled outbound variants/QR assets;
3. manage editable destinations where appropriate;
4. ingest platform-native reports;
5. map native campaign/sub IDs into a common taxonomy;
6. keep redirect clicks separate from marketplace-authoritative orders/GMV/commission;
7. produce normalized operator/client reports.

### Evidence supporting feasibility

- TikTok exposes affiliate/creator/seller data through partner APIs and export-style endpoints.
- Marketplace affiliate systems already use identifiers such as Sub ID, meaning there are potential join keys/workflows.
- Community anecdotes show multi-affiliate operations often become spreadsheet/reporting-heavy.

### Evidence against / risk

- TikTok Affiliate API access requires application/approval and is not active by default.
- Shopee exact API scopes/access for the desired Thailand workflow are unverified.
- Platform schemas, permissions and terms can change.
- Native platforms already provide valuable analytics; normalization must save enough work or improve decisions enough to justify another tool.
- The more LK01 depends on platform data, the more its product availability depends on external gatekeepers rather than only its own infrastructure.

### UNKNOWN / REQUIRED BEFORE LOCKING THIS OPTION

- Can WSTERA obtain TikTok Partner/API approval for the exact product model?
- Can WSTERA obtain sufficient Shopee API/export access?
- Which native identifiers can be legally/technically joined across systems?
- How much manual work remains after platform APIs are used?
- Who pays for the normalized view?
- Does the buyer need one platform, two platforms or many before the pain becomes material?

---

## 16. Privacy / PDPA / legal baseline

### VERIFIED — MARKET / REGULATORY BASELINE

Thai PDPA-oriented official guidance and government platforms emphasize:

- clear privacy notice and processing purpose;
- data minimization and retention controls;
- data-subject rights processes;
- processor/subprocessor governance;
- security and breach-management processes;
- safeguards for qualifying cross-border transfers;
- consent management where consent is the applicable legal basis.

### LK01 implications

The existing product decision not to persist raw IP as customer analytics and not to fingerprint users reduces privacy risk, but it does not eliminate it. Account data, click metadata, device/browser classes, platform IDs and imported order/campaign data may still be personal data depending on context and identifiability.

If LK01 later adds GA/Meta/TikTok pixels, audience tracking or tenant-injected tracking scripts, controller/processor roles and consent/cookie requirements become more complex and require a separate legal review.

Before public use, LK01 should expect to need at least privacy/terms, retention/deletion procedures, processor/subprocessor documentation and incident handling. Exact DPO, consent, cross-border and contractual obligations depend on actual processing design and must not be inferred from generic guidance alone.

### Tax baseline

Thai Revenue Department guidance states that businesses regularly selling goods/services in Thailand generally become subject to VAT registration when annual turnover exceeds ฿1.8 million, with registration timing rules after exceeding the threshold. Exact entity/tax treatment requires accountant/legal review.

Thai B2B buyers may also expect quotation, tax-invoice and withholding-tax workflows; local competitors such as WaanKit explicitly advertise business-document support. Whether LK01 needs those workflows in-product or through WSTERA billing remains open.

---

## 17. Abuse, phishing and domain-reputation burden

### VERIFIED — MARKET

Public URL-shortening infrastructure is an abuse target.

Major competitors maintain acceptable-use rules and abuse-reporting processes covering phishing, malware, spam, fraud and malicious redirects. Bitly's transparency reporting identifies malicious shortened links, especially phishing, as a major abuse class and describes dedicated trust/safety systems and external support.

### Consequence for LK01

A public self-serve short-link service has operational costs beyond hosting:

- automated abuse detection;
- malicious-destination blocking;
- customer/domain reputation protection;
- complaint/report channels;
- suspension and appeal procedures;
- incident/audit evidence;
- false-positive handling;
- potential browser/security-vendor blocklists.

### UNKNOWN

The likely abuse rate and support cost for a Thai-first LK01 cannot be estimated credibly before real traffic. Abuse operations must nevertheless be included in production economics and release design.

---

## 18. Product-structure options — intentionally unselected

The purpose of this section is to keep structurally different futures visible. The dossier does **not** choose among them.

### Option A — Current standalone branded-link + click-analytics SaaS

**Evidence supporting:**
- product contract already well documented;
- technically straightforward relative to deeper integrations;
- clear freemium subscription mechanics;
- local demand category demonstrably exists.

**Evidence against / risks:**
- heavy global and Thai competition;
- planned features are largely commoditized;
- local competitors already cover similar prices/workflows;
- economic buyer and WTP unproven;
- trust/safety burden exists for public short links.

**Primary evidence needed:** paid beta conversion/retention and explicit switch reason against current alternatives.

### Option B — Cross-platform campaign / affiliate operations standalone

**Evidence supporting:**
- native platforms create fragmented reporting silos;
- TikTok partner APIs prove some platform data can be programmatically accessed;
- multi-network operators have reconciliation/reporting work.

**Evidence against / risks:**
- API approval/gatekeeper risk;
- Shopee integration details unverified;
- native tools already provide strong single-platform analytics;
- higher implementation/maintenance complexity;
- payer/WTP unproven.

**Primary evidence needed:** real multi-platform workflows, time/cost lost today, partner API proof, paid pilot.

### Option C — Agency / MCN operations product

**Evidence supporting:**
- agencies/MCNs have multi-user/client/creator coordination needs;
- higher-value competitor plans cluster around teams, reporting, governance and automation;
- platform ecosystems formally recognize MCNs/partners.

**Evidence against / risks:**
- may become a substantially different product from current LK01;
- requires client/account permission design and deeper workflows;
- longer assisted-sales/support motion likely;
- no Thai agency/MCN primary evidence yet.

**Primary evidence needed:** agency/MCN interviews, workflow artifacts, buying authority, price acceptance and integration needs.

### Option D — Thai dynamic-QR / smart marketing touchpoint SaaS

**Evidence supporting:**
- clear offline/online use cases;
- recurring category exists locally;
- stable destination and QR are understandable jobs.

**Evidence against / risks:**
- WaanKit and other local tools already compete directly;
- one-off QR use can have weak monthly retention;
- likely feature creep into landing pages/forms/pixels/targeting.

**Primary evidence needed:** narrow underserved segment and recurring paid workflow not already met by local incumbents.

### Option E — Creator utility bundled into a wider creator suite

**Evidence supporting:**
- creators already use links as one part of commerce/content operations;
- bundling can create more recurring value than a standalone link tool.

**Evidence against / risks:**
- creator-suite category is crowded internationally;
- would materially expand scope beyond LK01;
- no evidence WSTERA should build a creator operating system.

**Primary evidence needed:** creator workflow research showing a bundle gap WSTERA can uniquely serve.

### Option F — LK01 as shared WSTERA link/redirect/analytics capability

**Evidence supporting:**
- core link/redirect/QR/analytics primitives can be useful inside other WSTERA products;
- avoids requiring a standalone acquisition engine if external WTP is weak;
- infrastructure work may be reusable internally.

**Evidence against / risks:**
- internal usefulness does not create standalone revenue;
- requires clear ownership/boundaries to avoid a shared-service maintenance sink;
- opportunity cost versus simply using an external provider must be measured.

**Primary evidence needed:** actual cross-product WSTERA demand, cost comparison, shared-service boundary and operational ownership.

### Option G — Internal capability only / pause standalone commercialization

**Evidence supporting:**
- avoids competing in a commoditized standalone market without WTP proof;
- can preserve useful redirect primitives for controlled WSTERA workflows.

**Evidence against / risks:**
- abandons potential external revenue before primary validation;
- prior product/market work becomes partially sunk cost;
- internal service still requires security/reliability maintenance.

**Primary evidence needed:** evidence that standalone paid demand remains weak after structured validation.

---

## 19. Decision-completeness tracker

| Question | Current confidence | What we know | What is still missing |
|---|---|---|---|
| Product/implementation reality | High | SoT and prototype inspected | production build evidence later |
| Global competitor/pricing landscape | High for review date | first-party pricing/features checked | future pricing changes |
| Thai competitor landscape | Medium-High | several direct products verified | full market census unnecessary but niche entrants may exist |
| Thailand digital-commerce baseline | High | authoritative/public structural data | LK01-specific addressable count |
| Native marketplace substitution | High for known features | Shopee/TikTok reporting is deeper than redirect clicks | exact user dependence/workflow by segment |
| Attribution technical limits | High | HTTP/referrer + UTM constraints verified | in-app/browser edge cases by platform if required |
| TikTok API technical existence | High | APIs and approval requirements documented | actual WSTERA approval and production scopes |
| Shopee API feasibility | Low-Medium | API surface exists | scopes, eligibility, terms, production access |
| Infrastructure/payment fee baseline | High for published vendor rates | current Cloudflare/Supabase/Stripe rates | real shared incremental WSTERA cost |
| Privacy/legal baseline | Medium | main obligation areas identified | counsel review against final data flows |
| Abuse/trust-safety burden | High as category risk | competitors prove material abuse class | LK01 incident/support rate |
| Economic buyer | Low | plausible roles mapped | actual budget owner |
| Buying trigger | Low | category triggers known | LK01-specific trigger |
| WTP | Low | category pricing exists | paid primary evidence |
| Pricing/package fit | Low | competitor benchmarks exist | price acceptance and retention |
| Acquisition/CAC | Unknown | proposed channels exist | experiments and conversion data |
| Repeat usage/retention | Unknown | recurring workflows hypothesized | cohort behavior |
| Support burden | Unknown | risk categories known | real tickets/time/cost |
| Platform partner approval probability | Unknown | approval required | actual application result |
| Standalone vs module/shared capability | Open | structural options mapped | requires buyer/WTP + portfolio economics |

---

## 20. What desk research cannot finish

A larger web search will not resolve the remaining decisive unknowns. They require primary evidence.

### A. Buyer / workflow evidence

Collect real current-state artifacts from target users, not hypothetical preference answers:

- channels/platforms currently used;
- actual link/campaign naming process;
- screenshots/export files/spreadsheets they already maintain;
- frequency of campaign changes;
- reporting cycle;
- who asks for the report;
- who approves software spend;
- time spent reconciling data;
- mistakes/lost work caused by current process;
- current paid tools and monthly cost.

### B. WTP evidence

Test a concrete offer with a real price and real commitment. Stronger evidence order:

`opinion < demo request < active pilot < price accepted < deposit/payment < renewal`

### C. Retention evidence

Observe at least two real operating/reporting cycles so repeat usage can be distinguished from novelty.

### D. Platform-access evidence

Prove data access directly:

- create/qualify required partner developer accounts;
- request TikTok Shop Affiliate scopes relevant to the chosen workflow;
- verify OAuth and real permitted data on test/authorized accounts;
- verify Shopee Affiliate/Open API eligibility and scopes;
- document rate limits, review requirements, terms and data-retention restrictions.

### E. Acquisition evidence

Measure at least one or more real acquisition routes rather than assuming content/community distribution will work. Capture traffic source, signup intent, activation and assisted-sales time.

---

## 21. Evidence collection cohorts — not product decisions

To avoid averaging incompatible buyers together, primary research should keep cohorts separate:

- individual creator/affiliate;
- seller/SME operator;
- agency/social admin;
- MCN/affiliate manager/partner.

A minimum research package should include enough cases per cohort to identify repeated workflow patterns; exact sample size should follow signal saturation rather than a fake statistical claim from a small qualitative study.

For product behavior evidence, real pilots should include actual traffic and actual reporting cycles, not demo-only sessions.

---

## 22. Questions reserved for Owner decision

Once the open evidence above is collected, the decision meeting should explicitly answer — rather than silently infer — these questions:

1. What exact job is LK01 being hired to do?
2. Who is the primary user?
3. Who is the economic buyer?
4. What event makes them start looking for a solution?
5. What do they use today?
6. Why is the current workaround insufficient?
7. What evidence shows they will pay rather than tolerate the workaround?
8. Is recurring subscription the correct commercial model?
9. What data must LK01 own versus import from authoritative platforms?
10. Is API dependence acceptable for the selected product structure?
11. What is the minimum recurring workflow that can support retention?
12. Does LK01 remain a standalone public SaaS, move toward an operations product, become a shared WSTERA capability, or stop standalone commercialization?
13. What historical Product Decisions must remain, be amended by ADR, or be retired after the Owner chooses?

No answer to these questions is locked by this dossier.

---

## 23. Current evidence boundary

### Desk-research package: substantially complete for decision preparation

The current evidence is sufficient to understand:

- what LK01 currently claims;
- what is and is not implemented;
- the direct global/local competitor pressure;
- marketplace-native substitute capabilities;
- attribution limits;
- current infrastructure/payment pricing shape;
- material API, privacy and abuse risks;
- the structurally different product futures available.

### Business decision package: not yet complete

The evidence is not sufficient to lock:

- primary economic buyer;
- final positioning;
- final pricing/package;
- willingness to pay;
- acquisition economics;
- retention;
- cross-platform API feasibility in WSTERA's own approved accounts;
- standalone vs module/shared capability.

Those remaining items depend primarily on user behavior, money and platform authorization rather than additional theoretical analysis.

---

## 24. Source register — external evidence checked 2026-09-17

### Competitors

- Bitly pricing: `https://bitly.com/pages/pricing`
- Rebrandly pricing: `https://www.rebrandly.com/pricing`
- Short.io pricing: `https://short.io/pricing`
- Dub links/pricing: `https://dub.co/pricing`
- Beacons pricing: `https://beacons.ai/i/pricing`
- URLkub: vendor pricing/product pages
- SHORTURL.IN.TH: vendor pricing/product pages
- WaanKit: vendor product/pricing pages
- nConnect ShortURL: `https://www.nc.co.th/shorturl/`

### Attribution

- MDN Referrer-Policy: `https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Referrer-Policy`
- Google Analytics custom campaign URL / UTM guidance: `https://support.google.com/analytics/answer/10917952`

### Infrastructure / payments

- Cloudflare Workers pricing: `https://developers.cloudflare.com/workers/platform/pricing/`
- Cloudflare for SaaS plans: `https://developers.cloudflare.com/cloudflare-for-platforms/cloudflare-for-saas/plans/`
- Supabase pricing: `https://supabase.com/pricing`
- Stripe Thailand pricing: `https://stripe.com/th/pricing`

### Thailand market/regulatory context

- OSMEP / SME Big Data public statistics
- ETDA e-commerce and SME digital-maturity publications
- DataReportal Digital 2026 Thailand
- Thai Revenue Department VAT guidance
- PDPC / GPPC privacy and data-governance guidance

### Platform ecosystems

- Shopee Thailand Affiliate Help Center / Sub ID / affiliate reporting materials
- Shopee Affiliate Open API surface
- TikTok Shop Partner Center Affiliate API documentation
- TikTok Shop Creator / Affiliate Link Performance documentation

### Community evidence

Reddit/Pantip discussions were used only as anecdotal workflow signals. They are not treated as representative market size, WTP, or buyer proof.

---

## 25. Relationship to existing research document

`docs/marketing/MARKET_POSITIONING_VALIDATION_2026-09-17.md` remains an earlier evidence review.

This dossier supersedes it only as the **broader decision-support evidence pack**. It does **not** supersede any canonical Product Truth or Owner decision.

Any eventual change to Product Vision, PRD, Product Decisions, pricing or positioning must occur only after Owner decision and the repository's required ADR/change-control process.
