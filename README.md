# iOS release runbooks

Step-by-step runbooks for shipping an iOS app (with optional iPad, Mac Catalyst, and iPhone Duo support) to TestFlight and the App Store, including in-app purchases and subscriptions.

They come from shipping a real app, [RoamReady](examples/roamready-1.0.md), for the first time in November 2026, and they record every place the process was confusing. Apple changes App Store Connect often. When a screen doesn't match a runbook, trust the screen and update the runbook.

## Which runbook when

| Situation | Read |
| --- | --- |
| New Apple Developer account, or first paid app on it | [01 Account setup](01-account-setup.md) |
| New app | [02 App record and capabilities](02-app-record-and-capabilities.md), then 03–09 in order |
| Adding subscriptions or in-app purchases | [03 In-app purchases](03-in-app-purchases.md), [04 Testing purchases](04-testing-purchases.md) |
| App Store screenshots | [05 Screenshots](05-screenshots.md) |
| Listing text, privacy label, age rating, compliance | [06 Listing and compliance](06-listing-and-compliance.md) |
| Any new build (TestFlight or App Store) | [07 Build, upload, TestFlight](07-build-upload-testflight.md) |
| Sending a version to App Review | [08 Submission and review](08-submission-and-review.md) |
| Approved, ready to go live | [09 Launch day](09-launch-day.md) |
| Something's wrong | [10 Gotchas](10-gotchas.md) |

## The whole flow, first release

```
Account (once)       Agreements, bank, tax ─ Sandbox tester ─ EU trader decision
App (once)           App ID + capabilities ─ App record ─ IAPs ─ Privacy ─ Age rating ─ Compliance ─ Pricing
Every release        Version bump ─ Archive ─ Upload ─ Encryption answer ─ TestFlight ─ Listing ─ Submit
Launch               Release ─ Offer codes ─ Check the live page ─ Release log
```

Order matters in a few places:

1. The **Paid Apps agreement** must be **Active** before in-app purchases work anywhere, TestFlight included. Start it on day one; it takes 1–2 days.
2. **Products** must be in the **same submission** as an app version the first time, and the **version goes into the draft first**.
3. A free app still needs a **price schedule** of **Free**.

## Templates

- [Release checklist](templates/release-checklist.md): print it and tick it off.
- [App Review notes](templates/app-review-notes.md)
- [TestFlight "What to Test"](templates/testflight-what-to-test.md)
- [Release log](templates/release-log.md)

## Conventions

- **(Xcode)**, **(ASC)** for App Store Connect, and **(device)** mark where a step happens.
- ⚠️ marks steps that can't be undone, or that blocked us when skipped.
- Never paste passwords, tax IDs, or bank details into chat tools or commit them. Enter them only on Apple's pages.
