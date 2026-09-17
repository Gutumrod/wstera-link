# LK01 Market & Positioning Validation — 2026-09-17

**Product:** WSTERA Link (LK01)  
**Status:** EVIDENCE REVIEW — recommendation only; does not override locked Product Vision / PRD  
**Research baseline branch:** `docs/hybrid-billing-promptpay`  
**Baseline SHA:** `ae7c4747473763e942d48807e1ac9576f42bc9bb`  
**Review date:** 2026-09-17

## 1. Executive conclusion

### VERIFIED
LK01 is still a pre-build product. The current repository explicitly states that no production application code exists and implementation remains on hold behind portfolio readiness/shared-boundary gates. The current business design is a Thai-first freemium subscription SaaS for branded campaign links and click analytics, with Free / Pro ฿199 / Business ฿590 plans.

The planned feature set is in a heavily commoditized market. Global products already provide branded links, custom domains, editable destinations, QR, UTM tools, analytics, APIs and team features; some free tiers are materially more generous than LK01's planned Free tier. Thailand already has direct local products covering the same jobs at similar or lower prices.

Shopee Thailand and TikTok Shop Thailand also provide native affiliate attribution that reaches beyond redirect clicks into orders, revenue/GMV, commission and traffic-source reporting. This weakens the current LK01 pain statement that affiliate operators lose measurement after sending traffic out of their own channel.

### RECOMMENDATION
**MARKET POSITIONING GATE: REMEDIATE BEFORE BUILD.**

Do not start the full current PRD implementation as a standalone product under the present positioning. The repository has a coherent technical contract, but there is not yet sufficient evidence for a defensible paid wedge.

The strongest remaining hypothesis to validate is **cross-platform campaign / affiliate operations and normalized reporting**, not generic short links or click analytics. That hypothesis is not yet validated and must not replace Product Truth until field evidence exists.

---

## 2. Current business model from Source of Truth

### VERIFIED
Current Product Vision defines LK01 as a **branded campaign-link and click-analytics SaaS** for Thai online sellers, creators, affiliate operators, agencies and small businesses. It explicitly says the product is not a generic URL shortener.

Current primary promise:

> Create a stable branded link, know which channel sends customers, and change the destination without replacing published links or QR codes.

Current intended jobs:
- Keep a public branded link stable while destinations change.
- Compare traffic sources by link/campaign.
- Change a destination after a link or QR is already distributed.
- Track outbound affiliate clicks before traffic leaves owned channels.
- Give owners enough evidence to decide where to invest effort.

Current monetization contract:

| Plan | Price | Active links | Tracked clicks / period | Analytics | Main paid differentiation |
|---|---:|---:|---:|---|---|
| Free | ฿0 | 5 | 250 | 7 days | custom slug, QR, 1 destination edit/link |
| Pro | ฿199/mo | 500 | 50,000 | 365 days | unlimited destination edits, campaign grouping, UTM builder, custom domain, CSV |
| Business | ฿590/mo | 5,000 | 500,000 | 730 days | Pro + API/Webhook + Team |

Payment rails are card recurring and PromptPay manual renewal through the portfolio centralized billing core. They are payment mechanisms, not separate revenue models.

### NOT VERIFIED
The repository does not establish a proven economic buyer. User segments are named, but it is not yet proven whether the payer is the individual creator, shop owner, marketing manager, agency, client of the agency, or another role.

No repository evidence currently proves repeat usage, retention, willingness to pay, paid conversion or a successful acquisition channel. The GTM document itself says those items still need validation.

---

## 3. Positioning versus implementation

### VERIFIED
The current production PRD describes a future multi-tenant Cloudflare-first TypeScript SaaS with Supabase Auth/RLS, quotas/entitlements, custom domains, campaign analytics, billing integration, API/webhooks and team access.

The code present today is a local Python/FastAPI + SQLite reference prototype. It can create/list short links, redirect them and show basic click/referrer analytics. It is not the production product.

Important gaps:

| Capability | Locked product contract | Current reference implementation |
|---|---|---|
| Short link / custom slug | Required | Present |
| Redirect | Required | Present |
| Basic click/referrer analytics | Required | Present, basic |
| Change destination | Core promise | Not present in exposed prototype API |
| QR | Core product | Not present |
| Campaign grouping / UTM builder | Pro | Not present |
| Custom domain | Pro | Not present |
| Multi-tenant Auth + RLS | Production requirement | Not present |
| Quota / entitlement / billing | Production requirement | Not present |
| CSV export | Pro | Not present |
| Team / API / webhook | Business | Not present as production feature |
| Non-blocking analytics hot path | Required | Prototype does synchronous click writes before redirect |
| No raw-IP analytics | Required | Prototype stores client IP |

Therefore current marketing positioning describes a planned product, not a capability that can be sold today.

---

## 4. Technical attribution constraint

### VERIFIED
LK01's own analytics specification already defines attribution precedence as:

1. explicit UTM source
2. normalized referrer source/hostname
3. `Direct / None`

and says unknown sources must not be guessed.

This is technically important because the HTTP `Referer` header is not guaranteed. Browser/site `Referrer-Policy` can reduce the referrer to origin-only or omit it entirely (`no-referrer`, cross-origin rules, downgrade rules, etc.). Google Analytics also documents that reliable campaign identification requires explicit campaign parameters such as `utm_source`, `utm_medium` and `utm_campaign`, with distinct source values for distinct platforms.

### CONSEQUENCE
The headline **“ลิงก์เดียว รู้ว่าลูกค้ามาจากไหน”** is broader than the technical guarantee.

If the exact same untagged short URL is posted across several channels and those channels do not provide a usable referrer, LK01 cannot deterministically infer the originating platform. Reliable source comparison requires source-specific tagged variants or another explicit signal.

A safer future promise would need to distinguish:
- redirect/click evidence LK01 itself can observe;
- explicit source tags that LK01 can control;
- native platform conversion attribution that LK01 cannot infer from a redirect alone.

This is consistent with the current PRD's non-claim that LK01 does not replace ad-platform attribution and must not claim conversion attribution without conversion evidence.

---

## 5. Competitor reality — global

Pricing/features below were checked on first-party product pages on 2026-09-17. Prices can change; they are evidence for this review date, not permanent constants.

| Product | Current evidence relevant to LK01 | Implication |
|---|---|---|
| Bitly | Free: 5 links/mo. Core $10/mo annual: 100 links, 30-day data, UTM builder and redirects. Growth $29/mo annual: 500 links, custom domain/branded links. Premium adds campaign-level tracking and deeper analytics. | Mature branded-link category leader already covers the core jobs. |
| Rebrandly | Free: 10 links/mo, unlimited clicks/scans, custom/free domain. Essentials starts around $8/mo annual with 250 links and 2 domains. Higher plans add destination edits, conversion tracking, webhooks, workspaces and teams. API is available broadly. | Branding, analytics, routing and collaboration are already mature. |
| Short.io | Free includes 5 custom domains, 1,000 branded links total and 50,000 tracked clicks/mo. Hobby $5/mo, Pro $18/mo, Team $48/mo in the current comparison table. | LK01 cannot defend Free/Pro solely by quota, custom domain or price. |
| Dub | Free includes 25 new links/mo, 1,000 tracked events/mo, 3 custom domains, API, UTM templates, QR and 30-day analytics. Current monthly Link plans list Pro $30, Business $90; Business adds conversion tracking, A/B testing, customer insights and event webhooks. | A modern competitor has moved beyond click analytics into conversion/partner infrastructure. |

### VERIFIED conclusion
`short link + QR + analytics + editable destination + custom domain + lower price` is not a defensible category position by itself.

---

## 6. Competitor reality — Thailand

The strongest challenge to “Thai-first” as a differentiator is that Thai/local products already exist.

| Product | Current first-party evidence | Direct overlap with LK01 |
|---|---|---|
| URLkub | Free 15 links + 15 QR/mo; Plus **฿199/mo** gives 200 links/QR, destination changes and UTM builder; Pro ฿399 adds deeper device/browser/country analytics. | Same headline Pro price as LK01 and same basic jobs. |
| SHORTURL.IN.TH | Pro **฿99/mo** lists 1 branded domain, tracking pixels, channels, campaigns, deep linking, targeting, A/B/rotator, API, import/export; Business **฿299/mo** lists unlimited URLs, 10 domains and 10 team users. Free marketing also claims unlimited basic short links/QR. | Undercuts LK01 on price while claiming a broader feature set. |
| WaanKit | Free dynamic QR/short links plus analytics; Starter ฿290/mo or ฿240/mo annual; paid plans add targeting, GA/Meta/TikTok pixels, forms and deeper reports; Enterprise offers custom domain/on-premise. | Strong dynamic-QR and offline/marketing workflow overlap. |
| nConnect ShortURL | Branded custom-domain short links, dashboard, referrer analytics, UTM builder, QR, multiple users, export/audit/data-ownership messaging. Cloud ฿2,990/year; self-hosting ฿5,950 one-time. | Direct Thai branded-link competitor with ownership/self-hosting angle. |

### VERIFIED conclusion
“ภาษาไทย / ราคาคนไทย / PromptPay / custom domain / QR / simple analytics” is not enough on current evidence to differentiate LK01.

PromptPay can reduce payment friction, but payment convenience is not the product-level reason to switch from existing link tools.

---

## 7. Native substitutes are stronger than the current affiliate pain statement

### Shopee Thailand — VERIFIED
Shopee Affiliate's own help center documents:
- dashboard reporting for clicks, orders, order rate, number of orders and estimated revenue, with CSV download;
- `Sub id` specifically for tracking promoted links, with results for link clicks and product orders;
- custom affiliate link construction that can carry referral source/custom values in `sub_id`, then preserve affiliate/UTM information after redirect.

This means a Shopee affiliate can already connect traffic identifiers with downstream order data inside the native affiliate system. LK01 V1 click analytics alone does not replace that value.

### TikTok Shop Thailand — VERIFIED
TikTok Shop's 2026 creator documentation says Affiliate Links can be shared outside TikTok and attributed to checkout. `Link Performance` shows GMV/items sold and traffic-source distribution, and current Creator Analytics documentation describes traffic-source data for GMV, clicks and items sold. Seller Affiliate Analytics exposes revenue, items sold, orders, buyers, estimated commission and platform traffic-source distribution.

This is materially deeper than LK01's planned V1 redirect analytics because it includes downstream commerce results.

### CONSEQUENCE
The current pain statement:

> “Affiliate ส่งคนออกจากช่องตัวเองแล้ววัดอะไรต่อไม่ได้”

is too broad for Shopee/TikTok Shop users in 2026.

There may still be a **cross-platform** reporting/operations problem, but that is a different hypothesis. It requires evidence that users actually suffer from reconciling multiple platform reports enough to pay for one normalized workflow.

---

## 8. Existing substitutes / workarounds

| Need | Existing substitute | Where it is enough | Remaining possible gap |
|---|---|---|---|
| Know source for owned website | GA4 + UTM | Own website / analytics property is controlled | Does not itself manage all outbound link assets |
| Affiliate click→order/revenue | Shopee/TikTok native affiliate analytics + Sub IDs | Platform-supported affiliate activity | Cross-platform normalization may remain manual |
| Basic short links / QR | Global/local free shorteners | Most low-volume users | No reason to pay LK01 |
| Dynamic printed QR | WaanKit / other dynamic-QR tools | Offline assets / campaigns | Already a mature paid category |
| Branded domain link | Short.io/Rebrandly/SHORTURL/nConnect etc. | Branding and redirect management | Commodity feature |
| Campaign organization | Tags/campaigns/workspaces in competitors, spreadsheets | Small teams can manage manually | Cross-platform operations might become painful at scale |
| Consolidated reporting | CSV/Sheets/manual exports or affiliate aggregators | Users comfortable with manual reconciliation | Potential hypothesis, not yet evidenced for LK01 ICP |

Community evidence is consistent with this: affiliate users commonly use platform-specific sub IDs and exported sheets; more advanced users seek centralized campaign/reporting tooling when multiple networks become hard to reconcile. This evidence is anecdotal and not Thai-specific, so it must not be treated as willingness-to-pay proof for LK01.

---

## 9. Revenue channels and willingness to pay

### VERIFIED monetization mechanics
The current repository monetizes through subscription plan limits/features. Paid triggers are designed around more links/clicks/retention plus custom domains, destination editing, campaign grouping, UTM, export, API/webhooks and team access.

### NOT VERIFIED willingness to pay
No current evidence proves that the intended LK01 customer will pay ฿199/month for those features rather than:
- use Short.io/Rebrandly/Dub free tiers;
- use Thai alternatives at ฿99–฿199;
- use native Shopee/TikTok attribution;
- use GA4/UTM for owned sites;
- use Sheets/CSV for reporting.

Feature gating is therefore a billing mechanism, not yet a validated buying reason.

### Evidence-backed buying reasons in the broader category
Current products and community evidence show that users do pay when their workflow reaches one or more of these thresholds:
- business-owned custom domains and brand control;
- high traffic / high-volume APIs;
- destination/routing controls;
- team/workspace governance;
- client or scheduled reporting;
- conversion/revenue attribution;
- reliability/SLA/security/compliance;
- data ownership or self-hosting;
- automation/webhooks/integrations;
- cross-network operational complexity.

LK01 has not yet proven which of these is strong enough for its specific Thai beachhead.

---

## 10. What is missing before positioning can be locked

### VERIFIED gaps
1. **Economic buyer definition** — user segments exist; budget owner/payer does not.
2. **Concrete buying trigger** — no evidence identifies the moment when a user switches from native/free tools to LK01.
3. **WTP evidence** — no paid pilot or other repository evidence demonstrates recurring willingness to pay.
4. **Defensible wedge** — current planned features are available globally and locally.
5. **Affiliate problem validity** — Shopee/TikTok native attribution contradicts the broad claim that outbound affiliate activity becomes unmeasurable.
6. **Attribution-message accuracy** — “one link knows the source” is not guaranteed by the current analytics contract.
7. **Production implementation** — product remains pre-build.
8. **Repeat-use / retention evidence** — not yet available.
9. **Acquisition-channel evidence** — GTM channels are planned, not proven.
10. **Cross-platform data access feasibility** — API/export rights, data schemas, automation constraints and terms for Shopee/TikTok/other platforms have not yet been established as a production contract.

---

## 11. Recommendation — do not expand the current shortener PRD yet

### RECOMMENDATION
Keep LK01 implementation on hold for product-market work even if portfolio infrastructure gates later become green.

Do **not** try to win by adding more commodity shortener features. Building the current full PRD first would create a smaller competitor to already mature global and Thai tools before proving a reason to switch.

### Best next hypothesis to validate
Reframe the discovery target as:

> **Cross-platform campaign / affiliate operations for Thai sellers and creators who currently reconcile links and performance across multiple channels or marketplaces.**

This is deliberately a **hypothesis**, not a new locked positioning statement.

Possible value loop to test without building the full SaaS:
1. Define one campaign once.
2. Generate controlled source-specific outbound link variants / QR assets.
3. Keep destinations centrally editable where technically appropriate.
4. Import or ingest native Shopee/TikTok/platform reports.
5. Normalize source/campaign identifiers into one view.
6. Show click evidence separately from platform-authoritative orders/GMV/commission.
7. Export a simple decision report for the creator/shop/agency.

This avoids claiming that LK01 can manufacture conversion truth from redirects. Native commerce platforms remain authoritative for their conversion data.

### Proposed validation gate (recommendation, not evidence)
Before authorizing a standalone product build:
- recruit 10 target users who actively use at least 2 relevant sales/affiliate/social channels;
- observe their current reporting/link workflow rather than only asking feature-preference questions;
- run a concierge/manual version using source-tagged links plus imported native reports;
- ask for actual payment, not only stated interest;
- require at least 3 real paid pilot users at the target entry price (currently ฿199/month) and repeat use across a second reporting cycle before treating the wedge as validated;
- record why non-paying users refuse and which existing tool/workaround wins instead.

If users consistently say native dashboards + Sheets are sufficient, LK01 should not continue as a standalone short-link SaaS under the current concept. At that point evaluate whether the redirect/link capability belongs as a shared module inside another WSTERA product rather than as an independent product.

---

## 12. Decision state

### VERIFIED
- Product concept/technical contract: clear.
- Current implementation: pre-build/reference prototype only.
- Target user segments: documented.
- Subscription mechanics: documented.
- Market: crowded globally and in Thailand.
- Native Shopee/TikTok attribution: materially overlaps the affiliate measurement story.

### ASSUMPTION / UNPROVEN
- Thai sellers/creators need a simpler link analytics tool enough to switch.
- ฿199 is a compelling paid threshold.
- PromptPay materially changes purchase behavior.
- Cross-platform reporting pain is severe enough for recurring payment.
- Agencies are a stronger payer than individual creators.

### RECOMMENDATION
**REMEDIATE positioning before build. Validate cross-platform campaign/affiliate operations as the next hypothesis. Do not modify locked Product Vision/PRD until that validation produces real evidence.**

---

## 13. Research method and limitations

Internal evidence was taken from the actual LK01 repository/branch and implementation reference files. External product facts were checked against first-party pricing/help/docs where available. Community material is treated as anecdotal, not market proof.

A Hermes research mission was attempted on the Windows Hermes runtime. The first run failed before tool use because the default `anthropic/claude-opus-4.6` model was routed to Ollama Cloud where that model did not exist. A second run used a per-run `deepseek-v4.1-flash` override without changing persistent configuration. It successfully re-read LK01 Source of Truth and began delegated evidence lanes, but the parent run stalled after dispatch and produced no contracted evidence bundle within its run budget. No unsupported Hermes claims were used in this document.

This review does not contain customer interviews, paid-pilot results or confidential platform partner/API access evidence. Those remain blockers to a final market-positioning lock.

---

## 14. External evidence sources checked 2026-09-17

### Global competitors
- Bitly pricing: https://bitly.com/pages/th/pricing
- Rebrandly pricing: https://www.rebrandly.com/pricing
- Short.io pricing: https://short.io/pricing/
- Dub Links pricing: https://dub.co/pricing/links
- Dub conversion tracking: https://dub.co/help/article/dub-conversions

### Thailand / local alternatives
- URLkub pricing: https://urlkub.com/pricing
- SHORTURL.IN.TH pricing: https://shorturl.in.th/pricing
- WaanKit pricing: https://www.waankit.com/pricing/
- nConnect ShortURL: https://www.nc.co.th/shorturl/

### Native affiliate/platform substitutes
- Shopee TH — Sub ID tracking: https://help.shopee.co.th/portal/10/article/163973
- Shopee TH — Affiliate dashboard/reporting: https://help.shopee.co.th/portal/10/article/123896
- Shopee TH — Custom affiliate short-link / sub_id flow: https://help.shopee.co.th/portal/10/article/172214
- TikTok Shop TH — Affiliate Links Guide for Creators: https://seller-th.tiktok.com/university/essay?knowledge_id=1653513000945425&lang=en
- TikTok Shop TH — Creator Analytics Overview: https://seller-th.tiktok.com/university/essay?knowledge_id=2213494138554129&lang=en
- TikTok Shop TH — Affiliate Analytics: https://seller-th.tiktok.com/university/essay?knowledge_id=6837801752971010&lang=en

### Attribution mechanics
- MDN Referrer-Policy: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Referrer-Policy
- Google Analytics campaign URL / UTM guidance: https://support.google.com/analytics/answer/10917952

### Anecdotal/community evidence — not market proof
- Reddit / AffiliateMarketing — SubID differences by network: https://www.reddit.com/r/Affiliatemarketing/comments/18a41pw
- Reddit / PartneredYoutube — unique links/SubIDs and spreadsheet/native reporting: https://www.reddit.com/r/PartneredYoutube/comments/1t2t2y2/
- Reddit / adops — high-volume user replacing expensive SaaS with private edge links: https://www.reddit.com/r/adops/comments/1r3on0r/
