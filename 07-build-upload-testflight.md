# 07 Build, upload, TestFlight (every release)

## Before archiving

- [ ] Code merged to `main` and pulled.
- [ ] Tests pass.
- [ ] CloudKit schema deployed to Production if the models changed ([02](02-app-record-and-capabilities.md#22-cloudkit-schema-if-the-app-syncs-with-cloudkit)).
- [ ] **Version** raised for an App Store release (`1.0.0` › `1.0.1` or `1.1.0`).
- [ ] Scheme › Run › Options › **StoreKit Configuration: None**.

## Archive and upload (Xcode)

1. Set the run destination to **Any iOS Device (arm64)**. **Archive** is greyed out while a simulator is selected.
2. **Product › Archive** (a few minutes). The **Organizer** opens.
3. **Distribute App** › **App Store Connect** (shown as "TestFlight & App Store") › keep the defaults (including **Manage Version and Build Number**) › **Distribute**.
4. The Organizer row should say **Uploaded to Apple**. Apple emails you when processing finishes, usually within 5–30 minutes.

## Export compliance ("Missing Compliance")

ASC › **TestFlight** › the build › **Manage** › "What type of encryption algorithms does your app implement?"

| Your app | Answer |
| --- | --- |
| Uses only encryption built into Apple's OS (HTTPS/URLSession, CryptoKit, Keychain, Data Protection) | ✅ **None of the algorithms mentioned above** |
| Bundles its own crypto library, or uses standard algorithms outside Apple's OS | Standard encryption algorithms… (more questions follow) |
| Proprietary or non-standard crypto | Proprietary… (documentation needed) |

The middle option's wording is confusing, but it means *your own* implementation, not Apple's. To skip the question on future uploads, add `ITSAppUsesNonExemptEncryption` = `NO` (Boolean) to `Info.plist`.

## TestFlight groups

- **Internal** (for example "Owner Testing"): up to 100 team members, **no review**, available as soon as processing finishes.
- **External** (for example "Family & Friends"): up to 10,000 people by email or public link. ⚠️ The first build of each version needs a short **Beta App Review** (hours to about a day). The build shows **Waiting for Review** until then.
- A new build joins **no group automatically**. Click the build › **Groups** › **+**.
- Fill in **Test Details › What to Test** ([template](templates/testflight-what-to-test.md)).
- Builds expire after **90 days**.

## Install and check (device)

TestFlight app › your app › **Install** (pull down to refresh). Check:

- [ ] Existing data survived the update.
- [ ] Sync works (the first build on **Production** CloudKit).
- [ ] Purchases work ([04](04-testing-purchases.md#stage-3-testflight)).
- [ ] The new feature works.

Feedback and crashes from testers appear under **TestFlight › Feedback**.
