# 08 Submission and App Review

App Store Connect gathers everything to review into a **Draft Submission** (the button at the bottom right of any page once a draft exists). The first time an app has in-app purchases, they **must** be reviewed **together with an app version**.

## The order that works

⚠️ **Add the app version first.** Adding products before the version created **several separate drafts**, with warnings like "add an app version for the selected platform".

1. **iOS App › version page** › check that the listing, build, and review info are filled in and saved › **Add for Review**. This creates the **iOS** draft, anchored to that version.
2. For each **new** product, open its page and click **Add for Review**:
   - the **subscription group**
   - **each subscription** in it (a group alone fails with "New subscription groups must be submitted with an auto-renewable subscription from within that group")
   - **each non-consumable or consumable**
3. Open **Draft Submission**. It should say "Items added below will be reviewed together with iOS version X", list **every item**, and show **no yellow warning**.
4. ⚠️ **Submit for Review** turns blue as soon as the version alone is in the draft. **Don't submit until the products are listed too**; otherwise the app is reviewed with an empty paywall, which is a common rejection.
5. **Submit for Review.** The status becomes **Waiting for Review**.

If drafts get messy, open each item and use **remove the item** (in its blue banner), then start again from step 1.

Later releases with no new products only need the version (step 1, then submit).

## The "In-App Purchases and Subscriptions" section

Older guides say to attach products in a section on the version page. That section only appears when products are in **Ready to Submit**. With the current draft flow, use **Add for Review** on each product instead (step 2).

## Review notes

Write them for someone who has never seen the app ([template](templates/app-review-notes.md)):

- Is sign-in needed? If yes, give a demo account.
- Where the paywall is, what's free, what's paid, and what happens without a purchase.
- Where **Restore Purchases** is.
- Anything hardware-dependent ("the Assistant only appears on devices with Apple Intelligence").

## After submitting

- **Waiting for Review** › **In Review** › **Pending Developer Release** (manual release) or **Ready for Distribution** (automatic). Usually 24–48 hours, with emails at each step.
- **Rejected or a question:** the details appear under **General › App Review** and by email, with a guideline number. Reply in App Store Connect, or fix and resubmit. A first submission getting a question is common.
- **Don't edit** the version or products while it's in review. Use **Cancel Submission** (on the submission page) if you must.
- The **app icon** in App Store Connect's header switches from the grid placeholder to your icon once the build is attached.
