# 10 Gotchas

Everything that confused or blocked the first release, with the fix.

| Symptom | Cause | Fix |
| --- | --- | --- |
| Paywall shows no plans or prices | Paid Apps agreement not **Active**, or a product missing metadata or availability, or (simulator) no StoreKit file selected | [01](01-account-setup.md), [03](03-in-app-purchases.md), [04](04-testing-purchases.md) |
| Xcode's Transactions window shows ⚠️ **Unfinished** | `.onInAppPurchaseCompletion` replaces StoreKit's automatic finish | Call `transaction.finish()` on verified results in the handler |
| Access didn't update after deleting a transaction in Xcode | Deletions send no notification | Test-only behavior. Expiry also sends none; the app catches it at the next foreground check |
| "File dimensions are invalid" | Screenshot from the wrong device size for the slot | Read the sizes under the slot; use iPhone 18 Pro (1206 × 2622) for the "medium display" slot |
| iPad simulator: "Requires a newer version of iPadOS" | Simulator runtime older than the deployment target | Use a simulator with a matching runtime |
| iPhone Duo inner screenshot is black | The device is folded | Unfold fully in the Simulator, and capture `--display=<inner UUID>` |
| Simulator stays in dark mode | The appearance change didn't apply to the app | Launch with the app's appearance key (`-appAppearance light`) |
| Weather icon crossed out in screenshots | Unsigned build has no WeatherKit entitlement | Build signed |
| "Missing Compliance" on a build | The export-compliance question | **None of the algorithms mentioned above** (Apple's OS crypto only); add `ITSAppUsesNonExemptEncryption = NO` |
| Several **Draft Submissions** | Products added before the app version | Remove them; add the version first, then the products |
| "New subscription groups must be submitted with an auto-renewable subscription" | Only the group was added | Add each subscription too |
| "Unable to Submit: add an app version" | The version isn't in the draft | Version page › **Add for Review** |
| Submit button blue but products missing | The version alone is enough to enable the button | Add the products **before** submitting |
| App icon is a grid placeholder in ASC and on sandbox purchase sheets | The app isn't live yet | Normal; it shows once a build is attached and after launch |
| Red EU banner on Business | DSA trader status not declared | Declare it, or exclude the EU ([01](01-account-setup.md#14-eu-digital-services-act-trader-status-asc--business--compliance)) |
| China "Missing Info" rows | China needs a security assessment and an AIGC filing | Exclude China, or complete them |
| Price Schedule empty on a free app | Free still has to be set | **Add Pricing › Free** |
| TestFlight subscription renewing "slowly" | TestFlight renews **daily** (up to six times) | That's expected; sandbox from Xcode is faster |
| Custom offer codes blocked | The product isn't approved yet | Create codes on launch day |
| Retention message body rejected | Over 144 characters | Shorten it |
| "Developer" menu missing in Settings | Developer Mode is off | Settings › Privacy & Security › Developer Mode |
| Device run says "Build succeeded" and nothing happens | Xcode is still extracting OS symbols | Wait 5–15 minutes with the phone unlocked |
| UI tests hang or "does not have a process ID" | The Mac is overloaded (load average in the hundreds) | Shut down extra simulators, then rerun |
| Manage-subscription sheet broke other sheets in the same view | `.manageSubscriptionsSheet` modifier conflict | Use `AppStore.showManageSubscriptions(in:)` |
| W-9 typo | The form locks on submit | Double-check before Submit; contact Apple to fix it |
