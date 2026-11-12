# SBlock Browser handoff

This directory tracks the SBlock Browser integration work against this Firefox/GeckoView source fork.

## Repository discovery
The connected GitHub account currently exposes:
- `sainip6501-wq/firefox` — Mozilla Firefox source fork (Fenix Android application).
- `sainip6501-wq/sainiott-cloudflare` — SainiOTT web project.

No separate SBlock Browser Android application repository was found. The standalone SBlock Android project is currently supplied as a ZIP in the ChatGPT conversation, so it is not yet part of this Git tree.

## Current branch
`sblock/android-ui-adblock-fix`

## SBlock issues confirmed from device screenshots
1. Android 15 / targetSdk 35 edge-to-edge insets are not applied to the custom home/browser roots, causing the status and navigation bars to overlap app controls.
2. The DNS dashboard showed 52 requests and zero blocked because the observed hosts were not in the conservative starter rules. DNS-only filtering cannot reliably separate server-side ad segments from the provider's video CDN.
3. The existing host-list extension is a starter filter, not a full EasyList/EasyPrivacy-compatible engine.

## Patch direction
- Apply system-bar and display-cutout insets to both home and browser root layouts.
- Keep the home service grid content-driven and avoid stretched/empty sections.
- Expand safe third-party ad/tracker host coverage, while avoiding blanket blocks for Prime Video/YouTube media delivery domains.
- Keep GeckoView tracking protection and the bundled extension; do not claim universal Chrome-extension compatibility.
- Treat the device DNS VPN as a limited fallback until IPv6, TCP DNS, encrypted DNS and packet handling are implemented and tested.

## Build gate
No release claim until Android Gradle compilation succeeds and the app is installed/tested on the target Android 13/15 devices. In particular, verify navigation-bar insets, home-card measurements, extension installation, real blocked-request counters, OTT login, playback, fullscreen and VPN consent.

This directory is a tracking/handoff record; it does not replace the standalone SBlock Android project.