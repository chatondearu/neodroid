# Vision & positioning

#product

## What this product is

**Neodroid** is a personal / community smartphone OS: a curated set of devices
running a coherent stack where **phone, SMS, wireless peripherals, sensors, and
chosen Android APKs** work day-to-day — without requiring Google services as a
core dependency. The product is not a universal ROM for every recent Android
phone; it is an OS that works well on **the maintainer's device(s) and devices
of people who choose to adopt it**.

## Audience

- **Primary users**: the project author; early adopters who accept a short
  supported-device list and some app/banking friction.
- **Operators / admins**: the same people building and flashing images (no
  separate ops org yet).

## Goals (product priorities)

1. Cellular **voice + SMS/MMS** (or modern RCS only if reliable without Google).
2. **Bluetooth** audio (headphones / earbuds) and other wireless connectivity
   the user relies on (Wi‑Fi, BT peripherals).
3. **Sensors** needed for a usable phone (accel, gyro, proximity, etc. —
   device-dependent).
4. Run **chosen Android APKs** (sideload / F-Droid / APK installs) — full Google
   Play / GMS is optional, not a goal.
5. **Camera** — desirable for daily use; may lag other priorities on early ports.
6. **NFC contactless payment** via a **licensed** wallet path (bank app,
   Curve-like, etc.) — not Google Wallet cloning. Investigate early; may force
   stack choice (see [[../architecture/nfc-contactless-payments|NFC payments]]).

## Non-goals (for now)

- Supporting **all** recent Android smartphones out of the box.
- Shipping Google Mobile Services / Google Wallet as a first-class dependency.
- Reverse-engineering or reimplementing Google Wallet / scheme bypass
  ([[../features/out-of-scope|out-of-scope]]).
- Building a new mobile kernel from scratch for arbitrary SoCs.
- Perfect Play Integrity / banking apps that require stock OEM attestation
  (mitigate case-by-case).

## Open product questions

- Preferred primary hardware (model / SoC) for v0.
- Stack: custom Android ROM vs Linux mobile (+ Waydroid) vs Mobile NixOS —
  see [[../architecture/os-landscape|OS landscape]].
- **Wallet comfort bar:** is “any working tap-to-pay app” enough, or is
  **Google Wallet specifically** required? (If the latter → stay near stock
  Android; deep custom OS has little payoff.)

## Related

- [[../architecture/must-haves|Must-haves checklist]]
- [[../architecture/os-landscape|Existing projects & inspiration]]
- [[../architecture/nfc-contactless-payments|NFC / tap-to-pay]]
- [[../features/index|Feature catalog]]
- [[../decisions/ADR-001-curated-device-set|ADR-001]]
