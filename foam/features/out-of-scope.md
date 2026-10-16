# Out of scope

Conscious product exclusions. Check here before re-proposing.

## Universal recent-Android support

- **Ruled out:** 2026-10-14 — product discussion → [[../decisions/ADR-001-curated-device-set|ADR-001]] (proposed)
- **Why:** Per-device kernel/blob cost; “boots via GSI” ≠ usable phone (modem, BT, camera, NFC).
- **Revisit if:** A Treble/GSI-only tier is explicitly scoped as best-effort, separate from supported devices.
- **Refs:** [[../decisions/ADR-001-curated-device-set|ADR-001]], [[../product/vision|vision]]

## Google Mobile Services as a core dependency

- **Ruled out:** 2026-10-14 — vision drafting
- **Why:** Not a product goal; users do not need Google stack for identity of the OS.
- **Revisit if:** A critical must-have APK has no alternative without GMS (evaluate per app).
- **Refs:** [[../product/vision|vision]], [[../architecture/must-haves|must-haves]]

## Unofficial Google Wallet clone / payment-network bypass

- **Ruled out:** 2026-10-14 — product discussion
- **Why:** Contactless pay is gated by **Visa/Mastercard/bank tokenization and
  scheme contracts**, not by Wallet UI code. Reverse-engineering or reimplementing
  Wallet to tap without those systems is illegal, unsafe, and would not produce
  working terminal payments. Neodroid will not pursue this.
- **Revisit if:** — (never as a DIY crypto/RE project; only via licensed
  wallet partners or bank apps)
- **Refs:** [[../architecture/nfc-contactless-payments|NFC payments]]

## Operate an open-source bank / FOSS Visa replacement for merchant NFC

- **Ruled out:** 2026-10-14 — product discussion
- **Why:** FOSS “core banking” ≠ acceptance network. Merchant EMV NFC requires
  scheme membership and regulation; out of scope for a phone OS. A2A / local
  cashless (SEPA Instant QR, Fedow-class) are adjacent ideas, not Neodroid v0.
- **Revisit if:** Product explicitly splits into a separate fintech venture with
  legal entity + PSP partners; not as part of the OS roadmap.
- **Refs:** [[../architecture/nfc-contactless-payments|NFC payments]]
