# Release checklist

Copy this into an issue or note for each release. Skip the **First release only** items afterward.

## Account (first app only)
- [ ] Paid Apps agreement, bank account, and tax form all **Active** ([01](../01-account-setup.md))
- [ ] Sandbox tester created; Developer Mode on the test phone
- [ ] EU trader decision made (declare trader, or exclude the EU)

## First release only
- [ ] Bundle ID and capabilities; app record created ([02](../02-app-record-and-capabilities.md))
- [ ] Products created with prices, availability, localization, review screenshots, and Family Sharing decided ([03](../03-in-app-purchases.md))
- [ ] Subscription levels set; free trial added; grace period on
- [ ] Retention message (optional), **added to the same draft as the version**; offer code offer created (codes come on launch day)
- [ ] Purchases tested: simulator (StoreKit file) › device (sandbox) › TestFlight ([04](../04-testing-purchases.md))
- [ ] Screenshots for every slot at the sizes the slot lists ([05](../05-screenshots.md))
- [ ] Privacy label matches the privacy manifest; age rating; content rights; category ([06](../06-listing-and-compliance.md))
- [ ] App Compliance: China, EU, medical handled
- [ ] Price Schedule set (**Free** counts); availability set; Mac-on-Apple-silicon decided
- [ ] Featuring nomination (optional)

## Every release
- [ ] Merged and pulled `main`; tests pass
- [ ] CloudKit schema deployed if the models changed
- [ ] Version raised; scheme StoreKit Configuration set to **None**
- [ ] Archived and uploaded; export compliance answered ([07](../07-build-upload-testflight.md))
- [ ] Internal TestFlight group added and installed; data, sync, and purchases checked
- [ ] What to Test filled in; external group added (Beta App Review)
- [ ] Version page: What's New, build, review notes, **manual release**
- [ ] Draft Submission: **version first**, then any new products; every item listed; submit ([08](../08-submission-and-review.md))

## Launch
- [ ] Release This Version ([09](../09-launch-day.md))
- [ ] Offer codes generated and shared
- [ ] Live page checked; one real purchase
- [ ] Release log updated
