# 09 Launch day

Status: **Pending Developer Release**.

1. **Release.** Version page › **Release This Version**. It appears on the store within a few hours, and search indexing can take up to a day.
2. **Offer codes:** now possible, since the product is approved and the app is Ready for Distribution ([03](03-in-app-purchases.md#35-offer-codes-free-or-discounted-access-for-friends-press-and-influencers)):
   - Product › **Offer Codes** › your offer › **Create Custom Codes** (code, **redemption limit**, expiry) or **Create One-Time Use Codes** (a count, then download the file).
   - Share `https://apps.apple.com/redeem?ctx=offercodes&id=<APP_APPLE_ID>&code=<CODE>`.
3. **Check the live product page** on a device:
   - [ ] Price ("Free" with "In-App Purchases")
   - [ ] Subscription prices and the free trial in the in-app purchase list
   - [ ] Screenshots in order, on each device type
   - [ ] Privacy label and age rating
   - [ ] Badges (for example **Optimized for iPhone Duo**)
4. **Buy it once yourself**, then cancel or ask for a refund if you like.
5. **Record the release** in the project's [release log](templates/release-log.md): version, build, commit, date, schema changes.
6. **Announce.** Keep the TestFlight groups for future betas.

## Follow-ups worth tracking

- Regions you excluded (EU, China) and what each needs.
- Platforms not shipped yet (for example the Mac).
- Featuring nomination dates.
- The first reviews and crash reports (ASC › **Ratings and Reviews**, Xcode Organizer › **Crashes**).
