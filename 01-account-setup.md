# 01 Account setup (once per Apple Developer account)

Do this once. A second app on the same account skips it.

## 1.1 Apple Developer Program

1. Enroll at [developer.apple.com/programs](https://developer.apple.com/programs) ($99/year) as an **Individual** or an **Organization** (an organization needs a D-U-N-S number).
2. Your name, or the organization's, appears as the seller on the App Store.

## 1.2 Agreements, bank, and tax (ASC › Business)

Needed for anything that takes money, **including in-app purchases in a free app**. ⚠️ Until all three are **Active**, StoreKit returns **no products**, even in TestFlight, and your paywall shows no prices.

1. **Business** (top menu) › **Agreements** › **Paid Apps Agreement** › **View and Agree to Terms**.
2. **Bank Accounts** › **+**. Use an account in your own name (or the organization's). Enter the routing and account numbers only on Apple's page.
3. **Tax Forms** › **+** › **U.S. Form W-9**, for a U.S. person:

   | Field | What to enter |
   | --- | --- |
   | 1. Name | Exactly as on your tax return |
   | 2. Business name | Blank, unless you file under a registered business name |
   | 3. Type of beneficial owner | **Individual/Sole proprietor** (or your entity type) |
   | 4. Exemption status | **Non-Exempt Payee** (individuals are not exempt) |
   | 5. Address | Your current mailing address |
   | 6. TIN | **SSN**, or an **EIN** if you have one for the business |
   | Part II | Read the certification; usually nothing to cross out |

   ⚠️ The form **can't be edited after Submit**. A name and number mismatch can cause **24% backup withholding**. This isn't tax advice; ask a professional if you have an LLC or anything unusual.

   Outside the U.S., you fill in a W-8BEN (individual) or W-8BEN-E (entity) instead.

4. Wait for **Paid Apps Agreement**, **Bank Account**, and **Tax Form** to all show **Active** (usually 1–2 days; you'll get an email).

## 1.3 Sandbox test account (ASC › Users and Access › Sandbox)

A fake buyer for testing real products from Xcode on a device.

1. **Test Accounts** › **+**.
2. Fields:
   - **Name:** anything.
   - **Email:** must look real and **must not already be an Apple Account**. Nothing is sent to it. A plus-alias of your own address works well (`you+apptest@example.com`). Never use your real Apple Account.
   - **Password:** a **new** one you don't use anywhere else, saved in your password manager.
   - **Country:** the storefront you want to see prices for (for example **United States**).
3. **Clear Purchase History** (same page) resets the tester, so you can test a free trial again. Each account gets only one trial per subscription group.

On the device:

1. **Settings › Privacy & Security › Developer Mode** › on. The phone restarts; confirm **Turn On** afterward.
2. **Settings › Developer** (now at the bottom of Settings) › **Sandbox Apple Account** › **Sign In** with the tester. Your real Apple Account stays signed in for everything else.

## 1.4 EU Digital Services Act: trader status (ASC › Business › Compliance)

Apple won't distribute in the **27 EU member states** until you declare whether you're a **trader** under the DSA. Business pages show a red banner until you do.

- **Trader** = acting for business purposes. Selling subscriptions or paid unlocks usually counts.
- A trader's **name, address, phone number, and email** are verified by Apple and **shown publicly on the EU product page**.
- **Non-trader** = no commercial intent (a hobby or free app). Declaring non-trader for a paid app risks removal from EU stores.

Options:

1. **Declare trader with business contact details** (recommended for paid apps): a **PO box or virtual mailbox**, a **separate business phone** (for example Google Voice), and a **support email**. Apple verifies the phone and email, which takes about a day.
2. **Leave the EU out at launch:** untick the 27 EU countries in Pricing and Availability ([06](06-listing-and-compliance.md#pricing-and-availability)), and add them later.
3. **Declare non-trader:** only if you truly aren't selling anything.

The 27 EU states: Austria, Belgium, Bulgaria, Croatia, Cyprus, Czechia, Denmark, Estonia, Finland, France, Germany, Greece, Hungary, Ireland, Italy, Latvia, Lithuania, Luxembourg, Malta, Netherlands, Poland, Portugal, Romania, Slovakia, Slovenia, Spain, Sweden. **Not** included: the UK, Norway, Iceland, and Switzerland.

This is a legal decision. The runbook only explains the options.
