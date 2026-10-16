# Mobile OS landscape (research)

#architecture

First research pass (2026-10-14). Inspiration and building blocks — not a stack
decision yet.

## Two routes

| Route | Base | APKs | Device breadth |
| ----- | ---- | ---- | -------------- |
| **A — Custom Android** | AOSP / Lineage-class | Native | Wider via Treble/GSI; still per-device trees |
| **B — Linux mobile** | Mainline (or Halium) + Linux UI | Via **Waydroid** (container) | Narrow; modem/camera often incomplete |

Neodroid vision does **not** require Android as identity — only calls, messaging,
wireless, sensors, and chosen APKs. That keeps both routes open.

## A — Android custom (examples)

| Project | Why look at it |
| ------- | -------------- |
| **AOSP** | Upstream baseline |
| **LineageOS** | Community port process, device trees, OTA patterns |
| **TrebleDroid / phh GSI** | Generic system images on Treble devices |
| **GrapheneOS** | Hardening / security bar (Pixel-focused) |
| **CalyxOS, /e/OS, iodéOS, DivestOS** | De-Googled product packaging |
| **Evolution X / crDroid** | Feature/customization ROMs |

**APK install:** native. Google Wallet still often blocked without GMS +
attestation (see [[nfc-contactless-payments]]).

## B — Linux mobile (examples)

| Project | Why look at it |
| ------- | -------------- |
| **postmarketOS** | Best community device encyclopedia; `pmbootstrap`; Phosh / Plasma / Sxmo |
| **Mobian** | Debian phone images |
| **Ubuntu Touch (UBports)** | Halium path (vendor Android kernel) |
| **Droidian** | Debian + Halium |
| **Sailfish OS** | Commercial model; Android app compatibility layer |
| **PureOS / Librem** | Hardware + OS coupled |
| **Waydroid** | De-facto APK runtime on Linux (Lineage-based image) |

**APK install:** Waydroid. Banking / Play Integrity / NFC passthrough are weak
spots. Camera and modem quality vary heavily by device.

## C — NixOS mobile

| Project | Status (research snapshot) |
| ------- | -------------------------- |
| **[Mobile NixOS](https://mobile.nixos.org/)** | Experimental; **mainline-only** (vendor Android kernels dropped as supported path) |
| Supported-ish devices | PinePhone / Pro, OnePlus 6 (`enchilada`), some Chromebooks; sparse published artifacts |
| Community ports | Occasional device flakes (e.g. tablet ports) — proof of possibility, not product |

**Fit for Neodroid:** attractive for declarative builds **if** primary hardware
is mainline-capable. Unattractive as a “any recent Android phone” strategy —
already rejected by [[../decisions/ADR-001-curated-device-set|ADR-001]], so Nix
remains viable **once a device is chosen**.

## UI / shell references

- Phosh, Plasma Mobile, Sxmo (Linux)
- AOSP SystemUI / Lawnchair-class launchers (Android)
- Phoshdroid (Linux-in-APK on stock Android) — reverse inspiration only

## Likely inspiration shortlist for Neodroid

1. **Device/port process** — LineageOS *or* postmarketOS (depending on route A/B).
2. **Declarative images** — Mobile NixOS / Nix flakes (if route B + Nix).
3. **APK bridge** — Waydroid (Linux) or native package manager (Android).
4. **Security packaging** — GrapheneOS ideas if staying on Android.
5. **Product framing** — /e/OS-style “complete phone OS” without Google core.

## Not decided

Stack A vs B vs Mobile NixOS. Blockers for the decision:

- Chosen primary device(s) and mainline/vendor kernel reality
- NFC payment path feasibility ([[nfc-contactless-payments]])
- Which APKs must run (list TBD — banking, messaging, etc.)

## References

- https://mobile.nixos.org/devices/
- https://github.com/mobile-nixos/mobile-nixos
- https://postmarketos.org/
- https://waydro.id/
