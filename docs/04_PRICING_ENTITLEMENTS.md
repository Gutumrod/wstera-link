# WSTERA Link — Pricing & Entitlements

**Status:** LOCKED pre-build baseline

## Plans
| Entitlement | Free | Pro | Business |
|---|---:|---:|---:|
| Price/month | ฿0 | ฿199 | ฿590 |
| Active links | 5 | 500 | 5,000 |
| Tracked clicks/period | 250 | 50,000 | 500,000 |
| Analytics visibility | 7 days | 365 days | 730 days |
| Custom slug | Yes | Yes | Yes |
| QR | Yes | Yes | Yes |
| Destination changes | 1/link | Unlimited | Unlimited |
| Campaign grouping | No | Yes | Yes |
| UTM builder | No | Yes | Yes |
| Custom domain | No | Yes | Yes |
| CSV export | No | Yes | Yes |
| API/Webhook | No | No | Yes |
| Team | No | No | Yes |

## Usage Period
Free usage resets monthly on an authoritative server-defined period boundary. Paid usage resets on the persisted subscription billing-period boundary. Client clocks never reset quota.

## Subscription States
`free | trialing | active | past_due | grace_period | cancel_at_period_end | cancelled | expired`

V1 launches without promotional trial unless separately approved later.

## Upgrade
- Upgrade only after verified provider event and persisted authoritative subscription transition.
- Existing current-period usage carries forward; upgrade raises ceiling, it does not erase usage.

## Payment Failure
- `past_due` starts a 7-day grace period.
- During grace, existing paid features/redirects remain usable and UI requests payment recovery.
- Grace expiry without recovery transitions to Free enforcement.

## Cancellation
Cancel-at-period-end keeps paid entitlement through paid-through timestamp, then transitions to Free unless reactivated authoritatively.

## Downgrade
- Existing active links continue redirecting even if over lower-plan active-link ceiling.
- New/reactivated links are blocked until within limit or upgraded.
- Analytics visibility follows current plan immediately.
- Paid-only metadata stays stored but management access is locked.
- Current-period counted usage is not reset by downgrade/upgrade.

## Custom Domain Downgrade
Paid→Free gives 7-day domain-routing grace. During grace routing continues but management is locked except removal/recovery. After grace, custom hostname routing is disabled while default `go.wstera.com` links remain valid.

## Manual Overrides
Admin-only, time-bounded where possible, auditable, reason-required, never client-supplied. Permanent commercial exceptions require an explicit plan/contract decision.

## Authority
Provider webhook + persisted subscription transition is authoritative. Browser return pages/query parameters/client metadata cannot grant entitlement. Duplicate/out-of-order events must be idempotent and cannot regress newer valid state.
