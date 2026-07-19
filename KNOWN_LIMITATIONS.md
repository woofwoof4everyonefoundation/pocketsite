# Known Limitations

Pocket Site is a v1 contest build focused on a temporary local garage-sale catalog.

- Visitors must be able to reach the host phone over the designated sale Wi-Fi or hotspot. Guest networks may block device-to-device traffic.
- Pocket Site does not create or configure `PocketWiFiSale`; the host does that in phone or router settings before opening the sale.
- Local IP addresses can change when Wi-Fi or hotspot state changes. The host can return to Pocket Site and use **Retry local connection**, or enter a verified local URL override.
- An Android foreground service and ongoing notification keep an Open catalog available while the host switches apps or locks the screen. Android may still reclaim the process in exceptional system conditions, and device Wi-Fi sleep behavior can vary.
- The catalog uses unauthenticated HTTP on a private local network. It is not intended for sensitive information.
- Public internet hosting is intentionally out of scope. Visitors outside the sale network cannot open the local URL.
- The visitor page supports browsing, categories, availability ordering, and automatic refresh; interactive filtering/search is not included in v1.
- Optional photos use Android document-picker URI access. A moved, deleted, or access-revoked source image may no longer display.
- The generated APK is a debug/test build signed with a local debug key. It is for judging and local archival, not production distribution through an app store.
- There are no accounts, payments, offers, messaging, reservations, marketplace discovery, maps, cloud sync, analytics, or advertising.
