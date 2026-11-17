# 04 Testing purchases

Test in this order. Each stage proves something the earlier one can't.

| Stage | Where | StoreKit Configuration (Xcode › Product › Scheme › Edit Scheme › Run › Options) | Account | Proves |
| --- | --- | --- | --- | --- |
| 1 | Simulator | **your `.storekit` file** | none | The code works. No ASC setup or agreement needed. |
| 2 | iPhone from Xcode | **None** | sandbox tester | Real ASC products load: IDs match, prices and the trial show. Needs the Paid Apps agreement **Active**. |
| 3 | TestFlight | (ignored) | **your own** Apple Account, never charged | The archived build works end to end. |

⚠️ Set the scheme back to **None** before device testing and before archiving. The StoreKit setting is saved in the shared scheme; don't commit it unless the whole team wants it.

## Stage 1: simulator with the `.storekit` file

1. Run the app. Delete it first for a clean onboarding.
2. The paywall should show every plan with its price and "1 week free", plus the one-time purchase.
3. **Take the review screenshot now** (Simulator › **File › Save Screen**). Use it for every product's Review Information.
4. **Debug › StoreKit › Manage Transactions** opens a window listing purchases:
   - A ⚠️ with **State: Unfinished** means your code never called `finish()`. Fix it ([03](03-in-app-purchases.md#32-code-checklist-storekit-2-no-server)).
   - **Refund** or **Expire** a purchase to test lapsing. Deleting a transaction in this window sends no notification, so the app only notices on its next entitlement check. That's test-only behavior.
5. Checklist:
   - [ ] Without a purchase: locked features open the paywall; saved data stays readable.
   - [ ] Trial or purchase: features unlock right away.
   - [ ] Expire or refund: back to locked, and nothing is lost.
   - [ ] One-time purchase: unlocks, and the status shows lifetime.
   - [ ] Restore with nothing bought: "No purchases found".

## Stage 2: device sandbox

1. Set the scheme to **None**. Sign in to the sandbox tester on the device ([01](01-account-setup.md#13-sandbox-test-account-asc--users-and-access--sandbox)).
2. Run from Xcode on the device.
   - The first run on a new iOS version spends **5–15 minutes** on "Extracting OS library symbols". Keep the phone unlocked and connected.
   - If the app doesn't launch, check that **Developer Mode** is on.
3. The paywall shows your **ASC** prices. If it's empty, the agreement isn't Active, or a product is missing metadata or availability.
4. Buy the trial. Sandbox renewals are accelerated; you can change the speed in **Settings › Developer › Sandbox Apple Account › Manage › Subscription Renewal Rate**.
5. Log noise to ignore: `Could not convert value introductory to event format` (StoreKit's own logging), CoreData debug lines, and network chatter.

## Stage 3: TestFlight

- Purchases use **your own** Apple Account, are marked **[Sandbox]**, and are **never charged**.
- ⚠️ TestFlight subscriptions **renew once a day, up to six times**, then expire. The free week is compressed to about a day.
- To test a lapse: **Settings › Apple Account › Subscriptions** › cancel. Access continues until the period ends.
- The app icon on the purchase sheet is a **blank placeholder** until the app is live. That's normal.
- Check that existing data survived. TestFlight is the first build that uses the **Production** CloudKit database.
