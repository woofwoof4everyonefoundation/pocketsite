# Submission Notes

## Build

- Project: Pocket Site
- Platform: Android, Kotlin, Jetpack Compose
- Minimum Android version: Android 10 / API 29
- Build command: `./gradlew assembleDebug`
- Verification: `./gradlew lintDebug`
- APK: `app-debug.apk`

The packaged APK is a debug/test artifact for contest judging. Android may require uninstalling an older Pocket Site debug build if that build was signed with a different local debug key.

## Product summary

Pocket Site is a temporary, local-first catalog for a physical event. A garage-sale host opens a catalog and displays PocketWiFiSale QR/instructions; nearby visitors browse a read-only page and see availability updates. Closing or deleting the sale stops local serving.

> Marketplace helps strangers find an item. Pocket Site helps people browse a temporary place.

## Judge setup

1. Install `app-debug.apk` on an Android 10+ host phone.
2. Create or select a local network/hotspot and connect host and visitor devices.
3. Launch Pocket Site and tap **Load Demo Sale**.
4. Open the sale and allow notifications.
5. Use the displayed URL or QR on the visitor device.

See `DEMO_SCRIPT.md` for the sub-three-minute recording flow and `KNOWN_LIMITATIONS.md` for local-network constraints.

## AI collaboration

Pocket Site was developed collaboratively with Codex powered by GPT-5.6. AI assistance supported product planning, Kotlin/Compose implementation, persistence, local HTTP and foreground-service work, QR workflows, tests, build diagnostics, stability investigation, and scope review. Product direction and final acceptance remained human-directed.
