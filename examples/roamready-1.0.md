# Worked example: RoamReady 1.0

The real values used for the first App Store submission of RoamReady (a SwiftUI camping planner for iPhone, iPad, Mac Catalyst, and iPhone Duo) on November 16, 2026. Use it as a reference for what "filled in" looks like.

## Business model

A free download, then **RoamReady Pro**:

| Product | Type | ID | US price | Trial |
| --- | --- | --- | --- | --- |
| Monthly | Auto-renewable, group "RoamReady Pro" | `com.tannerdev.roamready.pro.monthly` | $4.99 / month | 1 week free |
| Yearly | Auto-renewable, same group | `com.tannerdev.roamready.pro.yearly` | $34.99 / year | 1 week free |
| Lifetime | Non-consumable | `com.tannerdev.roamready.pro.lifetime` | $99.99 | — |

- Family Sharing on for all three.
- Without Pro, the app is **read-only**: saved data stays visible offline, while adding, editing, and the AI Assistant open the plans. Deleting and erasing always work.
- Plans appear once after onboarding, from a **Read-only** row on Home, and from Profile › RoamReady Pro (status, Manage subscription, Restore purchases).
- Retention message: header "Your trips stay with you"; body "Everything you've saved stays readable. Come back anytime to keep planning."
- Offer: "Friends & Family" on Lifetime (free; codes to be created at launch).

## Listing

- **Name:** RoamReady: Camping Planner. **Subtitle:** Camping trips, ready offline.
- **Category:** Travel / Lifestyle. **Age rating:** 4+.
- **Keywords:** `rv,camper,campground,checklist,trailer,motorhome,tent,booking,meal,grocery,weather,campsite,glamping` (exactly 100).
- **Privacy label:** Data Not Linked to You: **Coarse Location** (App Functionality), sent to Apple Weather and Apple Maps.
- **Availability:** 136 of 175 countries. **EU excluded** (DSA trader status deferred) and **China excluded** (security assessment and AIGC filing not done).
- **Mac:** a separate Catalyst version, planned later; "iPhone and iPad apps on Apple silicon Macs" unticked.
- **Screenshots:** 6 iPhone (1206 × 2622), 3 iPad 13" (2064 × 2752), and 6 iPhone Duo (3 cover at 1398 × 2034, 3 inner at 2853 × 2007), captured from an in-memory demo library with a debug flag.
- **Featuring nomination:** App Launch, mentioning iPhone Duo support.

## Timeline

| Date | Step |
| --- | --- |
| Nov 14 | Paid Apps agreement, bank, and W-9 submitted; products created; StoreKit code merged |
| Nov 16 | Agreement Active; device sandbox test passed; `1.0.0 (1)` archived and uploaded; TestFlight (Owner Testing, then Family & Friends); listing, privacy, age rating, compliance; nomination; **submitted** (version + group + Monthly + Yearly + Lifetime in one submission) |

## Bugs found during release testing

1. **Unfinished transactions:** paywall purchases weren't finished, because `.onInAppPurchaseCompletion` disables StoreKit's automatic finish. Fixed by finishing verified results in the handler.
2. **The Manage-subscription sheet modifier** broke another sheet in the same list (a UI test caught it). Replaced with `AppStore.showManageSubscriptions(in:)`.
3. **The Assistant was reachable without Pro.** Gated its entry points; the button stays visible and opens the plans.
