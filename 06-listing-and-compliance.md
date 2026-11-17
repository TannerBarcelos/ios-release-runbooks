# 06 Listing, privacy, age rating, compliance, pricing

All in App Store Connect. The left sidebar has **General**, **App Store** (Trust & Safety, Growth & Marketing), **Monetization**, and **Featuring**.

## Version page text (iOS App › version › Product Page Information)

| Field | Limit | Tips |
| --- | --- | --- |
| **Promotional text** | 170 | Can be changed any time without review |
| **Description** | 4,000 | ⚠️ Must include the **subscription terms**: free trial, then renews automatically unless cancelled at least 24 hours before the end of the period, managed in Apple Account settings. Add a **Terms of Use** link (Apple's standard EULA: `https://www.apple.com/legal/internet-services/itunes/dev/stdeula/`). |
| **Keywords** | 100, comma-separated, no spaces | **Don't repeat** words from the name or subtitle; they're already indexed. Use singular forms. |
| **Support URL** | | Required. A GitHub issues page works. |
| **Marketing URL** | | Optional |
| **Copyright** | | `2026 Your Name` |
| **Build** | | **+** › choose the uploaded build |
| **App Review Information** | | Sign-in not required (unless it is), your contact details, and the [review notes](templates/app-review-notes.md) |
| **Version Release** | | **Manually release this version** gives you control of launch day |

Then **Save**. Don't click **Add for Review** yet; see [08](08-submission-and-review.md).

## App Information (General › App Information)

- **Name** (30) and **Subtitle** (30).
- **Category:** a primary and an optional secondary.
- **Content Rights:** "No", unless you show licensed third-party content. Apple frameworks (Maps, Weather) don't count.
- **License Agreement:** Apple's Standard License, unless you have your own.
- **Age Rating** › **Edit**. Answer honestly; a utility app with nothing mature comes out **4+** (with local equivalents such as Brazil "AL", Korea "ALL", Vietnam "00+").
  - Opening links in **Safari** isn't "unrestricted web access"; an in-app browser is.
  - Private user notes aren't "user-generated content shared with others".
  - If asked about **AI or a chatbot**, say yes and describe it plainly.
- Ignore these unless they apply: **Age Suitability URL**, **App Encryption Documentation** (only for custom crypto), **App Store Server Notifications** (only with a server), **App-Specific Shared Secret** (old receipt validation).

## App Privacy (Trust & Safety › App Privacy)

The "nutrition label". It must match your **privacy manifest** (`PrivacyInfo.xcprivacy`) and your actual behavior.

1. **Privacy Policy URL:** required. A public markdown file on GitHub works.
2. **Data Types** › **Get Started** › "Yes, we collect data", unless you truly collect nothing.
3. Tick only what leaves the device to you or a third party. For example: **Coarse Location**, if the app sends an approximate location to a weather or maps service.
4. For each type, answer: purpose (for example **App Functionality**), **linked to identity?**, **used for tracking?**
5. **Don't tick:** **Purchases**, if Apple handles them and you have no server; data that stays on the device or in the **user's own private iCloud**; on-device AI processing.
6. **Publish.**

## App Compliance (General › App Compliance)

| Item | What it means | What to do |
| --- | --- | --- |
| **China mainland: Security Assessment** | Required to distribute in China | Complete it, or **exclude China mainland** in Pricing and Availability |
| **China mainland: AI Generated or Synthetic Content** | Required if the app has AI or generative features | Same choice |
| **Digital Services Act** | EU trader status | See [01](01-account-setup.md#14-eu-digital-services-act-trader-status-asc--business--compliance) |
| **Regulated Medical Devices** | Medical or Health & Fitness apps | Usually not applicable |

"Missing Info" rows for regions you exclude don't block submission.

## Pricing and Availability (Monetization › Pricing and Availability)

- ⚠️ **Price Schedule** › **Add Pricing** › **Free** (or your price). **A free app still needs this set**; it starts empty.
- **App Availability** › **Manage:** tick the countries. Exclude **China mainland** and the **27 EU states** if you aren't ready for their requirements. Products follow the app's availability.
- **iPhone and iPad Apps on Apple Silicon Macs:** untick it if you'll ship a real Mac (Catalyst) version, or haven't tested the iPad app on a Mac. Once a Mac version is approved, it replaces the iPad app on Macs anyway.
- **Tax Category:** "App Store software" (the default).

## iPhone Duo badge and featuring

- The **Optimized for iPhone Duo** badge appears when the app is **built with the iOS 27.1 SDK or later** *and* **iPhone Duo screenshots** are submitted. There's no separate application. ([Apple](https://developer.apple.com/iphone-duo/prepare/))
- **Featuring › Nominations** › **+** › **App Launch** (or New Content): a title, publish date, description, and **Helpful Details**. Mention Duo or other new-platform support here. It doesn't guarantee featuring, but it's the official channel. Submit it a few weeks before the publish date.
