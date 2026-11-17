# 02 App record and capabilities (once per app)

## 2.1 Bundle ID and signing (developer.apple.com › Certificates, Identifiers & Profiles)

1. **Identifiers** › **+** › **App IDs** › **App**.
2. **Bundle ID:** explicit, reverse-DNS (`com.yourname.appname`). ⚠️ **It can't change after the first submission.**
3. Enable the capabilities the app needs, for example:
   - **iCloud** (CloudKit). Create a container such as `iCloud.com.yourname.appname`.
   - **Push Notifications** (CloudKit sync uses silent pushes).
   - **WeatherKit** (App Services tab). Weather calls fail without it, and unsigned simulator builds can't use it.
   - **In-App Purchase** is on by default.
4. In Xcode, select your **Team** under **Signing & Capabilities** and use automatic signing.

Keep personal signing settings (team ID, containers) in a **git-ignored** xcconfig (for example `Config/Local.xcconfig`), with a checked-in `.example` copy.

## 2.2 CloudKit schema (if the app syncs with CloudKit)

Xcode builds use the **Development** database; TestFlight and App Store builds use **Production**. They're separate.

1. Run a signed build and use every feature, so each record type and field gets created in Development. A field only appears once it's actually saved.
2. [CloudKit Console](https://icloud.developer.apple.com) › your container › **Development** › **Schema** › check the record types (SwiftData uses `CD_<Model>` / `CD_<attribute>`).
3. **Deploy Schema Changes** › read the review screen › **Deploy**.
4. ⚠️ Production only accepts **additions**. Never rename, retype, or remove a field afterward, and deploy **before** uploading a build that uses new fields.

## 2.3 App record (ASC › Apps › +)

1. **New App**. Platforms: iOS (add macOS for Catalyst or Universal Purchase).
2. **Name:** what shows on the App Store, up to 30 characters, and it must be unique store-wide. It can include a descriptor (`AppName: Short Description`).
3. **Primary language**, the **bundle ID** from 2.1, and a **SKU** (any internal ID, such as `appname`).
4. **User access:** Full Access.

Once a build with an icon is attached, the app icon appears in App Store Connect. Until then, it shows a grid placeholder; that's normal.

## 2.4 Version numbers (Xcode › target › General › Identity)

- **Version** (`MARKETING_VERSION`), such as `1.0.0`: what users see. It must go up for each App Store release.
- **Build** (`CURRENT_PROJECT_VERSION`), such as `1`: only has to go up within a version. Xcode's **Manage Version and Build Number** option bumps it at upload.
