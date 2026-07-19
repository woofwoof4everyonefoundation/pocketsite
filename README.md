# Pocket Site

> Marketplace helps strangers find an item. Pocket Site helps people browse a temporary place.

Pocket Site is a local-first Android catalog for temporary physical events, beginning with garage sales. One host creates an inventory, opens the sale, and displays PocketWiFiSale instructions and QR codes. Nearby visitors join the designated Wi-Fi and browse a read-only catalog in their browser. The host can update availability in real time, close the sale, and erase all local sale data when the event ends.

The garage-sale problem is simple: a roadside sign cannot show passersby what is actually available. Pocket Site turns that sign into a QR preview, helping someone decide whether to stop without creating another marketplace.

Pocket Site is not a marketplace. It has no buyer accounts, payments, messaging, offers, reservations, public discovery, maps, cloud sync, analytics, or advertising.

## Current v1

- Draft, Open, and Closed sale lifecycle
- Local Room persistence for sale and item data
- Item title, description, price, category, availability, and optional gallery photo
- Host-authored notes, contact handoff, and Looking For list
- Read-only responsive visitor catalog with automatic status refresh
- Phone-hosted local HTTP catalog protected by an Android foreground service
- PocketWiFiSale SSID/password instructions
- Wi-Fi join QR and local catalog QR
- Copyable physical-sign instructions
- Clear closed-sale visitor page
- Recording-ready 10-item demo sale
- Confirmed Delete All Sale Data reset

## Requirements and build

- Android Studio with Android SDK 36
- JDK 21
- Android device or emulator running Android 10 / API 29 or newer

```bash
./gradlew assembleDebug
./gradlew testDebugUnitTest
./gradlew lintDebug
```

The debug APK is generated under `app/build/outputs/apk/debug/app-debug.apk`.

For the complete recording flow and honest v1 constraints, see [DEMO_SCRIPT.md](DEMO_SCRIPT.md) and [KNOWN_LIMITATIONS.md](KNOWN_LIMITATIONS.md).

## Local catalog setup

Pocket Site does not create or configure a hotspot. Before opening the sale, the host manually creates a phone hotspot or guest Wi-Fi—by default named `PocketWiFiSale`—and connects the host phone to it when necessary.

Both host and visitor devices must be on a network that permits device-to-device traffic. Guest networks may isolate clients. Opening a sale starts an Android foreground service and persistent notification so the local catalog can remain available while the host switches apps or locks the screen. Android can still reclaim the process in exceptional conditions, and changing Wi-Fi/hotspot networks can invalidate the advertised IP. Returning to Pocket Site and tapping **Retry local connection** republishes the current address. A manual local URL override is available when Android detects the wrong interface or hotspot address.

No internet connection, account, cloud backend, or visitor app is required.

## Architecture

Pocket Site intentionally uses one Android app module and a small explicit flow:

```text
Compose host UI
    → InventoryViewModel
    → ItemRepository
    → Room database

Open sale state + Room item flow
    → generated read-only HTML
    → local HTTP server
    → visitor browser
```

ZXing Core generates QR bitmaps locally. Android's document picker supplies optional photo references without storage or camera permissions. Manifest permissions are limited to local networking, the connected-device foreground service, and its notification. Android backup is disabled so temporary sale, contact, and Wi-Fi data remain on the host device.

## Three-minute demo

1. From Draft, tap **Load Demo Sale**.
2. Open the sale and show its Open state.
3. Show PocketWiFiSale instructions, Wi-Fi QR, catalog QR, and sign text.
4. Open the catalog on a visitor phone connected to the sale Wi-Fi.
5. Point out the read-only label, available/sold ordering, notes, contact handoff, and Looking For section.
6. Mark an available item sold on the host.
7. Let the visitor page auto-refresh within eight seconds.
8. Close the sale and show the closed visitor message.
9. Confirm **Delete All Sale Data** and show the empty Draft state.

## Privacy and scope

Sale data is app-local and Android backup is disabled. Delete All Sale Data removes the Room sale/items, sharing state, and persisted photo-access grants. It never deletes original photos from the user's gallery.

The catalog is plain HTTP on a private local network and has no authentication. Do not use it for sensitive information. While a sale is Open, a foreground service owns the server and displays an ongoing notification. Closing the sale, stopping the local catalog, or deleting sale data stops the service and removes the notification.

## AI collaboration

Pocket Site was developed collaboratively with Codex powered by GPT-5.6. AI assistance supported product planning, Kotlin and Jetpack Compose implementation, Room persistence, local HTTP and QR workflows, tests, build diagnostics, and scope review. Product direction, constraints, testing decisions, and final acceptance remained human-directed.
