# 05 Screenshots

## Which sizes

⚠️ **Read the sizes listed under each slot in App Store Connect.** They change. In November 2026, the slots on the version page (**App Previews and Screenshots**) were:

| Slot | Simulator to use | Accepted size (portrait) |
| --- | --- | --- |
| **iPhone with Dynamic Island (medium display)** | iPhone 18 Pro (6.3") | **1206 × 2622** or 1179 × 2556 |
| **iPad 13" display** | iPad Pro 13-inch | 2064 × 2752 (2048 × 2732 also listed) |
| **iPhone Duo**, cover (outer) screen | iPhone Duo, **folded** | 1398 × 2034 |
| **iPhone Duo**, inner screen | iPhone Duo, **fully open** | 2007 × 2853 (2853 × 2007 landscape) |
| **Mac** (on the macOS version) | the Mac app | 2880 × 1800, 2560 × 1600, 1440 × 900, or 1280 × 800 |

- The 6.9" Pro Max size (1320 × 2868) was **rejected** ("File dimensions are invalid") because the slot wanted 6.3".
- 1–10 screenshots per slot; smaller device sizes can be left empty, since Apple scales down.
- The simulator's **runtime** must meet your deployment target. An older iPadOS runtime can't install the app.
- iPhone Duo screenshots become **required in April 2027** for apps built with the iOS 27.1 SDK or later. Submitting them earns the **Optimized for iPhone Duo** badge ([06](06-listing-and-compliance.md#iphone-duo-badge-and-featuring)).

## Make the data look good

Add a **debug-only launch flag** (for example `-app-store-screenshots`) that:

- Uses an **in-memory** store with realistic demo data: real place names, a trip in progress, some items checked off, a filled-in list. Your real data is never touched.
- Pins paid access on, so no paywall or "read-only" banners appear.

Use a **signed** build. Unsigned simulator builds can't use WeatherKit and similar services, and show broken states (a crossed-out weather icon).

## Capture commands

```bash
# Build once, signed, for any simulator
xcodebuild -project App.xcodeproj -scheme App -configuration Debug \
  -destination 'generic/platform=iOS Simulator' -derivedDataPath .derivedData-shots build

SIM=<UDID>   # from: xcrun simctl list devices
APP=com.you.app
xcrun simctl boot $SIM
xcrun simctl status_bar $SIM override --time 9:41 --batteryState charged --batteryLevel 100 --wifiBars 3 --cellularBars 4
xcrun simctl install $SIM .derivedData-shots/Build/Products/Debug-iphonesimulator/App.app
for p in location camera photos; do xcrun simctl privacy $SIM grant $p $APP; done   # no permission prompts
xcrun simctl location $SIM set 36.2509,-121.7836                                    # a pretty location
xcrun simctl launch $SIM $APP -app-store-screenshots -appAppearance light
xcrun simctl io $SIM screenshot shots/iphone/01-home.png
sips -g pixelWidth -g pixelHeight shots/iphone/01-home.png                          # check the size
```

Tips:

- **Light or dark mode:** if the app has an `@AppStorage` appearance key, pass it as a launch argument (`-appAppearance light`). Changing the simulator's appearance setting didn't stick.
- **Wait** a few seconds after navigating; screenshots can lag a frame behind taps.
- **Multi-display devices (iPhone Duo):** list the displays with `xcrun simctl io $SIM enumerate`, then capture each one with `xcrun simctl io $SIM screenshot --display=<UUID> out.png`. Fold or unfold the device in the Simulator window. A folded device captures its inner display as solid black.
- Put the shots in a **git-ignored** folder (`AppStoreScreenshots/`).
- Never use fake or test AI replies in a screenshot. Capture real on-device output, or leave AI out.

## Pick a story

Five or six shots, in the order a new user would care about them. RoamReady's order:

1. Home, with the current trip and live weather
2. Trip overview (booking, checklists)
3. Trip overview, lower half (meals, grocery, forecast)
4. A checklist, part done
5. Grocery list by store section
6. The map search (Camp Finder)

On iPad and Duo, use the split layouts: list beside detail, results beside the map.

## Other assets

- **Header** (Product Page › Header and Search Results), 3840 × 1646 or 5244 × 2950: **optional**. Submission works without it.
- **App previews** (video): optional.
- **Paywall review screenshot:** see [04](04-testing-purchases.md#stage-1-simulator-with-the-storekit-file).
- **Captions or frames** around screenshots: optional; plain screenshots are accepted.
