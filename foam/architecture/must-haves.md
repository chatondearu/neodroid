# Must-haves (v0 intent)

#product #architecture

Captured from product discussion (2026-10-14). Refines [[../product/vision|vision]].

## Hard requirements

| Need | Notes |
| ---- | ----- |
| Phone (cellular voice) | Modem + ofono/ModemManager/RIL stack depending on OS path |
| Messaging (SMS at minimum) | MMS/RCS nice-to-have; Google Messages not required |
| Bluetooth headphones / earbuds | BT audio profile (A2DP/HFP); device+firmware dependent |
| Other wireless connectivity | Wi‑Fi, BT LE peripherals as used daily |
| Sensors | Enough for UI/calls (proximity, accel, …); list per device |
| Chosen Android APKs | Not “every Play Store app”; apps the user continues to need |
| Install arbitrary APKs | Sideload without Google account requirement |

## Soft / nice-to-have

| Need | Notes |
| ---- | ----- |
| Camera | Daily photography; often the hardest mainline Linux piece |
| Google services | Explicitly low priority |
| NFC tap-to-pay | Desired; **feasibility depends on stack + bank** — see [[nfc-contactless-payments]] |

## Explicitly out of scope (for now)

| Item | Why |
| ---- | --- |
| Universal device coverage | [[../decisions/ADR-001-curated-device-set\|ADR-001]] — curated adopters only |
| Stock Google Wallet as requirement | Vendor-locked to GMS / certified devices |

## Success bar (informal)

A supported device boots Neodroid and can: place/receive calls, send/receive SMS,
pair BT earbuds, use Wi‑Fi, run the user's critical APKs, and (if NFC goal
accepted) complete at least one contactless payment path documented for that
device/bank combo.
