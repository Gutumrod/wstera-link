# LK01 Market & Positioning Validation — 2026-09-17

**Product:** WSTERA Link (LK01)  
**Status:** EVIDENCE REVIEW — recommendation only; does not override locked Product Vision / PRD or Owner direction  
**Remote research baseline:** `docs/hybrid-billing-promptpay` @ `ae7c4747473763e942d48807e1ac9576f42bc9bb`  
**Additional local evidence:** untracked `docs/BUILD-TO-SELL-EXECUTION-2026-09-06.md` on the same local branch  
**Review date:** 2026-09-17

## 1. Executive conclusion

### VERIFIED
LK01 remains a pre-production product: the remote repository has no production application implementation yet. The locked Product Vision describes a Thai-first branded campaign-link and click-analytics SaaS for sellers, creators, affiliates, agencies and small businesses.

A newer local, untracked Owner execution brief dated 2026-09-06 materially changes execution state from the older remote `CURRENT_STATUS.md`: it says the old portfolio slot hold is superseded by **BUILD-TO-SELL**, records Product PASS + Business/Market PASS as a credible pre-build thesis (explicitly not PMF or final-price proof), and authorizes **LK-SR-01 production scaffold only** as the immediate next ticket. The same brief explicitly says historical ฿199/฿590 pricing is not automatically approved public pricing and paid launch must wait for real WTP/package evidence.

External evidence gathered on 2026-09-17 shows that the currently planned feature set sits in a heavily commoditized market. Global products already provide branded links, custom domains, editable destinations, QR, UTM tools, analytics, APIs and team features; Thailand already has direct local products covering the same jobs at similar or lower prices.

Shopee Thailand and TikTok Shop Thailand also provide native affiliate attribution that reaches beyond redirect clicks into orders, revenue/GMV, commission and traffic-source reporting. That weakens one of LK01's current pain statements: that affiliate operators lose measurement after sending traffic out of their own channel.

### RECOMMENDATION
**MARKET POSITIONING REVIEW: REMEDIATE BEFORE PUBLIC POSITIONING / PAID FEATURE LOCK — while allowing the Owner-authorized LK-SR-01 scaffold to proceed.**

Do not rewrite Product Truth from this report alone. Do not stop the Owner-authorized production scaffold. However, do not treat the previous Business/Market PASS as proof that the current public positioning, historical pricing or full paid-feature package is validated.

The strongest remaining hypothesis to validate is **cross-platform campaign / affiliate operations and normalized reporting**, not generic short links or click analytics. This is only a discovery hypothesis and must not replace Product Truth until field evidence exists.

---

## 2. Source-of-truth and execution-state reconciliation

### Remote committed state — VERIFIED
`docs/CURRENT_STATUS.md` on `docs/hybrid-billing-promptpay` says LK01 is pre-build, no production application code exists, and implementation was held behind portfolio P0b/P1 shared gates.

### Newer local execution state — VERIFIED LOCAL, NOT COMMITTED
The local working tree contains an untracked file:

`docs/BUILD-TO-SELL-EXECUTION-2026-09-06.md`

It states:
- Owner direction: **BUILD-TO-SELL**; old portfolio slot hold is superseded for execution priority.
- Council: Product PASS; Business/Market PASS, where PASS means credible pre-build market thesis, not PMF or final-price proof.
- Historical ฿199/฿590 pricing must not be treated as automatically approved public pricing.
- Immediate next ticket: **LK-SR-01 Phase 0 production scaffold only**.
- Paid launch waits for real WTP/package evidence and independent production review.

### INTERPRETATION
The newer local file is operationally important but is not yet canonical remote evidence because it is untracked. This report therefore preserves both facts rather than silently choosing one:
- remote committed docs still describe the older hold;
- newer local Owner direction authorizes scaffold work;
- neither source claims PMF or validated public pricing.

This market review does **not** recommend deleting, editing or auto-committing that untracked local file.

---

## 3. Current business model from committed Product Truth

### VERIFIED
Current Product Vision defines LK01 as a **branded campaign-link and click-analytics SaaS** for Thai online sellers, creators, affiliate operators, agencies and small businesses. It explicitly says LK01 is not a generic URL shortener.

Current primary promise:

> Create a stable branded link, know which channel sends customers, and change the destination without replacing published links or QR codes.

Current intended jobs:
- Keep a public branded link stable while destinations change.
- Compare traffic sources by link/campaign.
- Change a destination after a link or QR is already distributed.
- Track outbound affiliate clicks before traffic leaves owned channels.
- Give owners enough evidence to decide where to invest effort.

The committed pricing baseline is:

| Plan | Historical baseline | Active links | Tracked clicks / period | Analytics | Main paid differentiation |
|---|---:|---:|---:|---|---|
| Free | ฿0 | 5 | 250 | 7 days | custom slug, QR, 1 destination edit/link |
| Pro | ฿199/mo | 500 | 50,000 | 365 days | unlimited destination edits, campaign grouping, UTM builder, custom domain, CSV |
| Business | ฿590/mo | 5,000 | 500,000 | 730 days | Pro + API/Webhook + Team |

**Important:** the newer local Build-to-Sell brief explicitly marks these historical paid prices/quotas as **unvalidated public pricing**. They remain useful as the committed baseline contract, not as a market-validated launch price.

Payment rails are card recurring and PromptPay manual renewal through the portfolio centralized billing core. Payment rails are not separate revenue models.

### NOT VERIFIED
The evidence does not establish a proven economic buyer. User segments are named, but it is not yet proven whether the payer is the individual creator, shop owner, marketing manager, agency, agency client or another role.

No reviewed evidence proves repeat usage, retention, willingness to pay, paid conversion or a successful acquisition channel. The GTM document and newer Build-to-Sell brief both leave WTP/package proof open.

---

## 4. Positioning versus implementation

### VERIFIED
The production PRD describes a future multi-tenant Cloudflare-first TypeScript SaaS with Supabase Auth/RLS, quotas/entitlements, custom domains, campaign analytics, billing integration, API/webhooks and team access.

The implementation present today is a local Python/FastAPI + SQLite reference prototype. It can create/list short links, redirect them and show basic click/referrer analytics. It is not the production product.

| Capability | Locked product contract | Current reference implementation |
|---|---|---|
| Short link / custom slug | Required | Present |
| Redirect | Required | Present |
| Basic click/referrer analytics | Required | Present, basic |
| Change destination | Core promise | Not present in exposed prototype API |
| QR | Core product | Not present |
| Campaign grouping / UTM builder | Paid baseline | Not present |
| Custom domain | Paid baseline | Not present |
| Multi-tenant Auth + RLS | Production requirement | Not present |
| Quota / entitlement / billing | Production requirement | Not present |
| CSV export | Paid baseline | Not present |
| Team / API / webhook | Business baseline | Not present as production feature |
| Non-blocking analytics hot path | Required | Prototype does synchronous click writes before redirect |
| No raw-IP analytics | Required | Prototype stores client IP |

Therefore the current marketing positioning describes a planned product, not a capability that can be sold today. LK-SR-01 is only the authorized production scaffold step in the newer local execution brief.

---

## 5. Technical attribution constraint

### VERIFIED
LK01's analytics specification defines attribution precedence as:
1. explicit UTM source;
2. normalized referrer source/hostname;
3. `Direct / None`.

Unknown sources must not be guessed.

The HTTP `Referer` header is not guaranteed. Browser/site `Referrer-Policy` can reduce the referrer to origin-only or omit it entirely. Google Analytics documents that reliable custom-campaign identification uses explicit parameters such as `utm_source`, `utm_medium` and `utm_campaign`, with distinct source values per platform/channel.

### CONSEQUENCE
The headline **“ลิงก์เดียว รู้ว่าลูกค้ามาจากไหน”** is broader than the technical guarantee.

If the exact same untagged short URL is posted across several channels and those channels do not provide a usable referrer, LK01 cannot deterministically infer the originating platform. Reliable source comparison needs a source-specific tag/variant or another explicit signal.

Future messaging must distinguish:
- redirect/click evidence LK01 itself observes;
- explicit source/campaign tags LK01 controls;
- native platform conversion truth that LK01 cannot infer from a redirect alone.

This matches the existing non-claims in Product Truth: LK01 does not replace ad-platform attribution and must not claim conversion attribution without conversion evidence.

---

## 6. Competitor reality — global

Pricing/features below were checked on first-party product pages on 2026-09-17. They are point-in-time evidence, not permanent constants.

| Product | Current evidence relevant to LK01 | Implication |
|---|---|---|
| Bitly | Free: 5 links/mo. Core $10/mo annual: 100 links, 30-day data, UTM builder and redirects. Growth $29/mo annual: 500 links, custom domain/branded links. Premium adds campaign-level tracking and deeper analytics. | Mature category leader already covers core jobs. |
| Rebrandly | Free: 10 links/mo, unlimited clicks/scans and a domain option. Essentials starts around $8/mo annual with 250 links and 2 custom domains. Higher plans add destination edits, conversion tracking, webhooks, workspaces and teams. | Branding, analytics, routing and collaboration are mature. |
| Short.io | Free includes 5 custom domains, 1,000 branded links total and 50,000 tracked clicks/mo. Current table lists Hobby $5/mo, Pro $18/mo and Team $48/mo. | LK01 cannot defend Free/Pro solely by quota, custom domain or price. |
| Dub | Free includes 25 new links/mo, 1,000 tracked events/mo, 3 custom domains, API, UTM templates, QR and 30-day analytics. Current Link plans list Pro $30/mo and Business $90/mo; Business adds conversion tracking, A/B testing, customer insights and event webhooks. | Modern competitors have moved past click analytics into conversion/partner infrastructure. |

### VERIFIED conclusion
`short link + QR + analytics + editable destination + custom domain + lower price` is not a defensible category position by itself.

---

## 7. Competitor reality — Thailand

The strongest challenge to “Thai-first” as differentiation is that Thai/local products already exist.

| Product | Current first-party evidence | Direct overlap with LK01 |
|---|---|---|
| URLkub | Free 15 links + 15 QR/mo; Plus **฿199/mo** gives 200 links/QR, destination changes and UTM builder; Pro ฿399 adds deeper device/browser/country analytics. | Same historical headline Pro price as LK01 and same basic jobs. |
| SHORTURL.IN.TH | Pro **฿99/mo** lists 1 branded domain, tracking pixels, channels, campaigns, deep linking, targeting, A/B/rotator, API and import/export; Business **฿299/mo** lists unlimited URLs, 10 domains and 10 team users. | Undercuts the historical LK01 Pro price while claiming broader features. |
| WaanKit | Free dynamic QR/short links plus analytics; Starter ฿290/mo or ฿240/mo annual; paid plans add targeting, GA/Meta/TikTok pixels, forms and deeper reporting; Enterprise offers custom domain/on-premise. | Strong dynamic-QR/offline marketing overlap. |
| nConnect ShortURL | Branded custom-domain links, dashboard, referrer analytics, UTM builder, QR, multiple users, export/audit/data-ownership messaging. Cloud ฿2,990/year; self-hosting ฿5,950 one-time. | Direct Thai branded-link competitor with ownership/self-hosting angle. |

### VERIFIED conclusion
“ภาษาไทย / ราคาคนไทย / PromptPay / custom domain / QR / simple analytics” is not sufficient on current evidence to differentiate LK01.

PromptPay may reduce payment friction, but payment convenience is not a product-level reason to switch.

---

## 8. Native substitutes weaken the current affiliate pain statement

### Shopee Thailand — VERIFIED
Shopee Affiliate's help center documents:
- dashboard reporting for clicks, orders, order rate, number of orders and estimated revenue, with CSV download;
- `Sub id` specifically for tracking promoted links, with results for link clicks and product orders;
- custom affiliate-link construction that can carry referral-source/custom values in `sub_id` and preserve affiliate/UTM information after redirect.

A Shopee affiliate can therefore connect traffic identifiers with downstream order data inside the native affiliate system. LK01 V1 click analytics alone does not replace that value.

### TikTok Shop Thailand — VERIFIED
TikTok Shop's 2026 creator documentation says Affiliate Links can be shared outside TikTok and attributed to checkout. `Link Performance` shows GMV/items sold and traffic-source distribution; current Creator Analytics describes traffic-source data for GMV, clicks and items sold. Seller Affiliate Analytics exposes revenue, items sold, orders, buyers, estimated commission and platform traffic-source distribution.

This is materially deeper than LK01's planned V1 redirect analytics because it includes downstream commerce results.

### CONSEQUENCE
The current pain statement:

> “Affiliate ส่งคนออกจากช่องตัวเองแล้ววัดอะไรต่อไม่ได้”

is too broad for Shopee/TikTok Shop users in 2026.

A **cross-platform** reporting/operations problem may remain, but that is a different hypothesis and requires evidence that reconciliation pain is large and recurrent enough to pay for.

---

## 9. Existing substitutes / workarounds

| Need | Existing substitute | Where it is enough | Remaining possible gap |
|---|---|---|---|
| Source on owned website | GA4 + UTM | Own analytics property is controlled | Does not manage all outbound assets |
| Affiliate click→order/revenue | Shopee/TikTok native analytics + IDs | Platform-supported affiliate activity | Cross-platform normalization may remain manual |
| Basic short links / QR | Global/local free shorteners | Most low-volume users | No reason to pay LK01 |
| Dynamic printed QR | WaanKit / dynamic-QR tools | Offline assets/campaigns | Mature paid category already |
| Branded-domain links | Short.io/Rebrandly/SHORTURL/nConnect etc. | Branding/redirect management | Commodity feature |
| Campaign organization | Tags/campaigns/workspaces + spreadsheets | Small teams can manage manually | May become painful at scale |
| Consolidated reporting | CSV/Sheets/manual exports/affiliate aggregators | Manual workflow accepted | Potential hypothesis, not yet LK01 evidence |

Community evidence is consistent with platform-specific Sub IDs, exports and spreadsheets being common workarounds; advanced users seek centralized campaign/reporting tooling when multiple networks become difficult to reconcile. This material is anecdotal and not Thai-specific, so it is not WTP proof.

---

## 10. Revenue and willingness to pay

### VERIFIED monetization mechanics
The committed baseline monetizes through subscription limits/features: more usage/retention plus custom domains, destination editing, campaign grouping, UTM, export, API/webhooks and team access.

### VERIFIED local override on pricing status
The newer local Build-to-Sell brief says historical `199/590` must **not** be treated as automatically approved public pricing. Therefore this review does not evaluate ฿199/฿590 as final launch prices; it uses them only to compare the old baseline against today's market.

### NOT VERIFIED willingness to pay
No reviewed evidence proves that the intended LK01 customer will pay a recurring price for the existing bundle instead of:
- global free tiers;
- Thai alternatives around ฿99–฿199;
- native Shopee/TikTok attribution;
- GA4/UTM for owned sites;
- Sheets/CSV/manual reporting.

Feature gating is a billing mechanism, not a validated buying reason.

Broader-category evidence shows buyers can pay for business-owned domains, high-volume APIs, advanced routing, team governance, client reporting, conversion/revenue attribution, reliability/SLA/security/compliance, data ownership/self-hosting, automation/integrations and cross-network operational complexity. LK01 has not yet proven which of those is the buying trigger for its beachhead.

---

## 11. Evidence gaps before public positioning/package lock

1. **Economic buyer** — documented users, unproven payer/budget owner.
2. **Concrete buying trigger** — no evidence identifies when a user abandons native/free/manual tools.
3. **WTP/package evidence** — explicitly still open in the local Build-to-Sell brief.
4. **Defensible wedge** — planned base features exist globally and locally.
5. **Affiliate pain validity** — Shopee/TikTok native attribution contradicts the broad “cannot measure after outbound” claim.
6. **Attribution-message accuracy** — one untagged link cannot always know platform source.
7. **Production implementation** — pre-production; immediate local ticket is scaffold only.
8. **Repeat-use / retention evidence** — not available.
9. **Acquisition-channel evidence** — GTM channels are plans, not demonstrated channels.
10. **Cross-platform data access feasibility** — API/export rights, schemas, automation constraints and platform terms are not yet a production contract.

---

## 12. Recommendation and execution boundary

### RECOMMENDATION
Respect the Owner Build-to-Sell direction and allow **LK-SR-01 Phase 0 production scaffold** to proceed because it is infrastructure/scaffold work and does not require pretending market validation is complete.

Do **not** use this research to auto-edit locked Product Vision, Pricing or PRD. Do **not** expand scope merely by adding more shortener features.

Before locking public positioning, public pricing/packages, or spending significant effort on paid-feature differentiation, run a focused validation on the strongest remaining hypothesis:

> **Cross-platform campaign / affiliate operations for Thai sellers and creators who currently reconcile links and performance across multiple channels or marketplaces.**

This is a hypothesis, not new Product Truth.

### Concierge validation loop
1. Define one campaign once.
2. Generate controlled source-specific outbound link variants/QR assets.
3. Keep destinations centrally editable where appropriate.
4. Import native Shopee/TikTok/platform reports manually first.
5. Normalize source/campaign identifiers into one view.
6. Separate LK01-observed clicks from platform-authoritative orders/GMV/commission.
7. Export a simple decision report for creator/shop/agency.

### Proposed validation gate — recommendation, not evidence
Before treating the new wedge as validated:
- recruit 10 target users actively using at least 2 relevant channels/platforms;
- observe their current workflow rather than ask only feature-preference questions;
- run the concierge/manual workflow across at least 2 reporting cycles;
- ask for actual payment, not stated interest;
- require at least 3 real paying pilot users around the intended entry price before locking a recurring plan;
- record why non-paying users refuse and which existing tool/workaround wins instead.

If native dashboards + Sheets are consistently sufficient, re-evaluate whether LK01 should remain a standalone SaaS. A shared redirect/campaign-link capability inside another WSTERA product may be more rational, but that would require a separate Owner/ADR decision.

---

## 13. Decision state

### VERIFIED
- Product/technical contract: clear.
- Current production state: not implemented; reference prototype only.
- Owner execution direction: newer local brief authorizes Build-to-Sell and LK-SR-01 scaffold.
- Target user segments: documented.
- Public pricing/WTP: explicitly not final/validated.
- Market: crowded globally and in Thailand.
- Shopee/TikTok native attribution: materially overlaps the current affiliate measurement story.

### ASSUMPTION / UNPROVEN
- Thai sellers/creators need another simple link-analytics tool enough to switch.
- Historical ฿199 is the correct entry price.
- PromptPay materially improves paid conversion.
- Cross-platform reconciliation pain supports recurring payment.
- Agencies are a stronger payer than individual creators.

### RECOMMENDATION
**Continue only the already-authorized scaffold work. Remediate/validate positioning and packages before treating the historical market thesis as a public sell-ready proposition. Validate cross-platform campaign/affiliate operations next; do not lock that hypothesis without real user/payment evidence.**

---

## 14. Research method and limitations

Internal evidence was taken from the actual LK01 repository, committed SoT documents, reference implementation and the newer untracked local Build-to-Sell brief. External product facts were checked against first-party pricing/help/docs where available. Community material is treated as anecdotal, not market proof.

A Hermes research mission was attempted on the Windows Hermes runtime. The first run failed before tool use because default `anthropic/claude-opus-4.6` was routed to Ollama Cloud where that model did not exist. A second run used a per-run `deepseek-v4.1-flash` override without changing persistent configuration. It re-read LK01 Source of Truth and began delegated evidence lanes, but the parent run stalled after dispatch and produced no contracted evidence bundle within its run budget. No unsupported Hermes claims are used here.

This review contains no customer interviews, paid-pilot results or confidential platform-partner/API access evidence. Those remain evidence gaps.

---

## 15. External evidence sources checked 2026-09-17

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
- Shopee TH — custom affiliate short-link/Sub ID flow: https://help.shopee.co.th/portal/10/article/172214
- TikTok Shop TH — Affiliate Links Guide for Creators: https://seller-th.tiktok.com/university/essay?knowledge_id=1653513000945425&lang=en
- TikTok Shop TH — Creator Analytics Overview: https://seller-th.tiktok.com/university/essay?knowledge_id=2213494138554129&lang=en
- TikTok Shop TH — Affiliate Analytics: https://seller-th.tiktok.com/university/essay?knowledge_id=6837801752971010&lang=en

### Attribution mechanics
- MDN Referrer-Policy: https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Referrer-Policy
- Google Analytics campaign URL / UTM guidance: https://support.google.com/analytics/answer/10917952

### Anecdotal/community evidence — not market proof
- Reddit / AffiliateMarketing — SubID differences by network: https://www.reddit.com/r/Affiliatemarketing/comments/18a41pw
- Reddit / PartneredYoutube — unique links/SubIDs and native reporting/Sheets: https://www.reddit.com/r/PartneredYoutube/comments/1t2t2y2/
- Reddit / adops — high-volume user replacing expensive SaaS with private edge links: https://www.reddit.com/r/adops/comments/1r3on0r/
