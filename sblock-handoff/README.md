# SBlock Browser handoff

This directory tracks SBlock Browser remediation against this Firefox/GeckoView source fork.

## Repository discovery
The connected GitHub account exposes:
- `sainip6501-wq/firefox` — Mozilla Firefox source fork (Fenix Android application).
- `sainip6501-wq/sainiott-cloudflare` — SainiOTT web project.

No separate SBlock Browser Android application repository was found. The standalone SBlock app is currently supplied as a ZIP in the ChatGPT conversation, so it is not yet part of this Git tree.

## Current branch
`sblock/android-ui-adblock-fix`

## Committed handoff files
- [Android edge-to-edge/system-insets patch](patches/2.1.2-system-insets.patch)
- [Additional conservative ad/tracker host rules](adblock-extra-hosts.txt)

These files document the changes to apply to the standalone SBlock project; they are not changes to Mozilla's Fenix source tree.

## Screenshot findings
1. Android 15 / targetSdk 35 edge-to-edge insets were missing from custom home/browser roots, allowing system bars to overlap app controls.
2. The DNS dashboard showed 52 requests and zero blocked because the observed hosts were not in the starter rules.
3. The host-list extension is a starter filter, not a full EasyList/EasyPrivacy-compatible engine.

## Safety boundaries
- Do not blanket-block Prime Video/YouTube media delivery domains; doing so can break playback.
- DNS-only filtering cannot reliably separate server-side ad segments from the provider's video CDN.
- IPv6, TCP DNS, DoH/DoT and hard-coded IP traffic can bypass the current DNS VPN.
- GeckoView WebExtensions are not universal Chrome-extension compatibility.

## Build gate
No release claim until Android Gradle compilation succeeds and the app is installed/tested on the target Android 13/15 devices. Verify system insets, home-card measurements, extension installation, blocked-request counters, OTT login/playback, fullscreen and VPN consent.

This directory is a handoff/patch record; it does not replace the standalone SBlock Android project.