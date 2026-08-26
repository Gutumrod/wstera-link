# WSTERA Link — Analytics Specification

**Status:** LOCKED pre-build baseline

## Counting Definitions
- **Redirect request:** request reaches a valid public link route.
- **Tracked click:** successfully resolved redirect that passes bot filtering and is accepted by analytics ingestion.
- **Quota click:** exactly one accepted `click.tracked`.
- Bot-filtered and quota-dropped events do not consume quota.
- Customer-facing Total Clicks = `click.tracked` inside selected/visible range.
- V1 does not claim unique visitors or unique clicks.

## Canonical Events
`link.created`, `link.destination_changed`, `link.disabled`, `link.enabled`, `redirect.requested`, `redirect.resolved`, `redirect.failed`, `click.tracked`, `click.bot_filtered`, `click.dropped_quota`, `domain.verified`, `domain.disabled`.

## Attribution
Precedence: explicit UTM source → normalized referrer source/hostname → `Direct / None`.
Original UTM source/medium/campaign may be retained as bounded strings. Unknown sources remain `Other`; do not silently guess platform identity.

## Bot Filtering
- Deterministic, versioned rules.
- Known crawler/preview/security scanner signatures may be excluded from tracked quota.
- Filtering never blocks redirect.
- Filter version is recorded in processing metadata/implementation evidence.

## Device Data
Normalize into coarse classes such as mobile/desktop/tablet/other and browser family. Do not expose raw fingerprinting data.

## Time
Persist timestamps in UTC. Tenant dashboard default display timezone is `Asia/Bangkok` in V1; architecture must permit future tenant timezone configuration.

## Quota Algorithm
1. Resolve redirect.
2. Normalize/filter event.
3. Atomically consume one unit for eligible event under tenant billing period.
4. If allowed: persist/aggregate `click.tracked`.
5. If exhausted: record only minimal operational `click.dropped_quota` metric if needed; do not create customer analytics detail.
6. Redirect response is unaffected.

## Aggregation
Maintain query-efficient daily aggregates by tenant/link/day/source plus bounded detail required for recent analytics. Aggregate recomputation must be deterministic from authoritative retained events where possible.

## Reconciliation
Dashboard numbers may differ from Facebook/TikTok/LINE because platforms use different bot, preview and attribution definitions. Product copy must say WSTERA Link counts redirects accepted by its own tracking rules, not promise parity with ad-platform counters.
