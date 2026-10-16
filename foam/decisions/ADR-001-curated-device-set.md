# ADR-001 — Curated device set (not universal Android coverage)

- **Status**: proposed
- **Date**: 2026-10-14
- **Tags**: #architecture #product

## Context

Building a phone OS that boots on “any recent Android smartphone” implies
endless per-device kernel/blob work (or fragile GSI-only support). The product
goal is a usable daily driver for the maintainer and voluntary adopters, not
market-wide hardware coverage.

## Decision

Neodroid targets a **curated, explicit device list**. A device is supported only
when phone/SMS, wireless (incl. BT audio), sensors needed for daily use, and
chosen APKs are verified on that hardware. Adopters buy or keep hardware from
that list (or contribute a port that meets the same bar).

## Alternatives considered

| Alternative | Why rejected |
| ----------- | ------------ |
| Support all Treble/GSI Android phones | “Boots” ≠ modem/camera/BT/NFC quality; support burden unbounded |
| Only PinePhone-class Linux-first hardware | May fail APK / NFC / camera expectations; keep as option per device, not exclusive |
| Delay device policy until stack is chosen | Device list and stack co-constrain each other; need the policy now |

## Consequences

- **Positive**: Finite porting scope; honest marketing; NixOS/mainline remains
  possible for chosen SoCs.
- **Negative**: Small addressable audience; device EOL risks.
- **Constraint**: Primary device(s) must be named before heavy implementation;
  each new model is a deliberate project, not an assumption.

## References

- [[../product/vision|Vision]]
- [[../architecture/os-landscape|OS landscape]]
- [[../architecture/must-haves|Must-haves]]
