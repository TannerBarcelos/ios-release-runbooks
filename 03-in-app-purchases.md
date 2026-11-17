# 03 In-app purchases and subscriptions

Two halves: the **code** (StoreKit 2) and the **products** (ASC). The product IDs must match **exactly** in the code, the local `.storekit` test file, and App Store Connect.

## 3.1 Decide the model first

Write it down before coding. Common shapes:

| Model | Products |
| --- | --- |
| Paid upfront | None. Set the app's price in Pricing and Availability. |
| Freemium | A free app, plus a subscription or non-consumable that unlocks features |
| Free trial, then paywall | Auto-renewable subscriptions with an introductory free offer |
| Lifetime option | A **non-consumable** next to the subscriptions |

Also decide what happens when access lapses. **Read-only** (data stays visible, editing needs a subscription) is friendly and passes review easily. Hiding a user's own data does not.

Apple requires subscriptions to provide **ongoing value** (guideline 3.1.2).

## 3.2 Code checklist (StoreKit 2, no server)

- [ ] Product IDs in one place, for example an enum: `com.you.app.pro.monthly`, `.yearly`, `.lifetime`.
- [ ] **At launch**, start a task that listens to `Transaction.updates`. It delivers renewals, refunds, Ask to Buy approvals, Family Sharing changes, and purchases from other devices. **Verify** each transaction and **`finish()`** it.
- [ ] Decide access from `Transaction.currentEntitlements`: verified only, and ignore any with a `revocationDate`. A lifetime purchase wins over a subscription.
- [ ] Re-check entitlements when the app returns to the foreground.
- [ ] Paywall: Apple's **`SubscriptionStoreView`** shows plans, the trial, **Restore**, and the policy links. Add `.storeButton(.visible, for: .restorePurchases)`, `.subscriptionStorePolicyDestination(url:for:)` for Terms and Privacy, and a `ProductView` for a one-time purchase.
- [ ] ⚠️ If you attach **`.onInAppPurchaseCompletion`**, StoreKit **stops finishing paywall purchases for you**. Finish verified transactions in your handler, or they show as **Unfinished** and get re-delivered on every launch.
- [ ] **Restore Purchases** button (`AppStore.sync()`), required by review.
- [ ] **Manage subscription:** `AppStore.showManageSubscriptions(in: windowScene)`. This worked better than the `.manageSubscriptionsSheet` modifier, which interfered with other sheets.
- [ ] If edits happen inside sheets, present the paywall from the **topmost view controller**. A root SwiftUI sheet can't appear over another sheet.
- [ ] Unit-test the access rules (lifetime wins, refunds don't count, unknown IDs ignored).
- [ ] A debug launch flag to pin access (`-store-ui-test full|read-only`) for UI tests and screenshots.
- [ ] A **StoreKit configuration file** (`.storekit`) with the same IDs, prices, trial, and Family Sharing setting.

Works offline: StoreKit 2 caches verified entitlements on the device. Expiry sends **no** notification; the app learns about it at the next entitlement check, which is fine for most apps.

## 3.3 Subscription group and subscriptions (ASC › Monetization › Subscriptions)

1. **Subscription Groups** › **Create** › reference name (for example `AppName Pro`).
2. On the group page:
   - **Display Name and Description** › **Create** › English (U.S.): the display name users see in **Settings › Subscriptions**. Set **App Name Display** to **Use App Name**.
3. **Subscriptions** › **Create** for each plan:
   - Reference name (`Monthly`), product ID, duration.
4. On each subscription page, top to bottom:
   - **Family Sharing** › **Turn On**, if wanted. ⚠️ **It can't be turned off** once live.
   - **Availability:** set up all countries. For yearly plans, set up **1 Year Upfront**. Leave **Monthly with a 12-Month Commitment** alone unless your app supports that checkout.
   - **Subscription Prices** › **Add Subscription Price** › base country and price › **Next**; review the automatic prices for other countries › **Confirm**.
   - **Introductory offer:** **View all Subscription Pricing** › **Introductory Offers** › **+** › all countries, start today, **no end date**, **Free**, **1 Week** (or your choice). Each person gets one per group.
   - **Retention messaging:** see 3.6.
   - **Display Name and Description:** English (U.S.).
   - **Image:** optional (1024 × 1024, used for win-back and offer code pages).
   - **Purchase Options** (multiseat) and **Tax Category:** leave as is.
   - **Review Information:** a **screenshot of the paywall** and a short note ("Unlocks X. Without it, Y."). Without the screenshot, the product stays at **Missing Metadata**.
   - **Save.**
5. **Levels** (group › Subscriptions › **Edit**): plans that unlock **the same thing** belong at the **same level**. Then switching between them is a crossgrade at the next renewal. At different levels, moving to the higher one is an immediate upgrade with a prorated refund.
6. On the Subscriptions page:
   - **Billing Grace Period** › **16 days**, all renewals, **Production and Sandbox**. Subscribers whose card fails keep access while Apple retries the charge.
   - **Streamlined Purchasing:** leave on.

⚠️ **Don't click Add for Review on a product until the app version is in the draft.** See [08](08-submission-and-review.md).

## 3.4 Non-consumable / lifetime (ASC › Monetization › In-App Purchases)

1. **Create** › **Non-Consumable** › reference name, product ID.
2. **Availability** › all countries.
3. **Price Schedule** › **Add Pricing** › price.
4. **Family Sharing** › Turn On, if wanted (permanent).
5. **App Store Localization:** display name and description.
6. **Review Information:** the paywall screenshot and a note.
7. **Save.**

## 3.5 Offer codes (free or discounted access for friends, press, and influencers)

- Apple **retired in-app purchase *promo* codes on March 26, 2026**. **Offer codes** replace them and work for **every product type**, including non-consumables.
- **You can create the offer** (product page › **Offer Codes** › **+**) before launch: reference name, **customer eligibility** (tick all three to include anyone), countries, and price (**Free**).
- ⚠️ **Codes can only be generated after the product is approved and the app is Ready for Distribution.** Do this on launch day ([09](09-launch-day.md)).
- **One-time codes:** unique and single-use. Apple generates a file of them.
- **Custom codes:** a memorable code (`FRIENDS26`) with a **redemption limit** and an expiry. Anyone who has it can use it, so cap the count. **Deactivate** stops it immediately; people who already redeemed it keep the item.
- Redemption: share `https://apps.apple.com/redeem?ctx=offercodes&id=<APP_APPLE_ID>&code=<CODE>`, or have people use App Store › profile › **Redeem Gift Card or Code**. In-app redemption uses `.offerCodeRedemption(isPresented:)`.
- A redeemed code arrives as a normal transaction, so the `Transaction.updates` listener unlocks it.
- **Sandbox codes** (same page) let you test redemption before launch.

## 3.6 Retention messaging (on a subscription page)

Shown on Apple's **Confirm Cancellation** screen.

- **Header:** a reason to stay, up to about 45 characters.
- **Body:** ⚠️ **under 144 characters**. Don't mention prices or offers in the text.
- **Image:** optional; 3840 × 2160 or 5244 × 2950.
- **Subscriptions & Offers:** attach to each plan; an offer is optional (it needs a promotional offer created first).
- ⚠️ It has its own **Add for Review**, and **it needs an app version in the same submission**. Add it to the first release's draft together with the products. If you forget, it waits in a draft until the next app version.
