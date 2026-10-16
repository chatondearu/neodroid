# NFC contactless payments

#architecture #product

Research note (2026-10-14). Answers: *can Neodroid users keep paying with their
card via phone NFC?*

## Short answer

| Goal | Realistic? |
| ---- | ---------- |
| Clone / emulate a **physical bank card** secret onto the phone without the bank | **No** (by design — secrets stay in the card chip) |
| **Reverse-engineer Google Wallet** to pay without Google / schemes | **No — out of scope** (see [[../features/out-of-scope|out-of-scope]]). Terminals talk EMV with **tokenized credentials issued by banks/networks**, not with APK UI logic |
| **Google Wallet / Google Pay** on a custom OS or Linux+Waydroid | **Usually no** (GMS + Play Integrity / certified device) |
| **Bank or third-party wallet app** that supports HCE on a custom **Android** ROM | **Sometimes yes** (bank- and country-dependent; GrapheneOS users report Curve, some EU banks, PayPal, etc.) |
| NFC payments inside **Waydroid** on Linux mobile | **Effectively no / unreliable** today (host NFC not properly exposed to the container) |
| Keep a **physical card** or **watch** for tap-to-pay | Always a fallback |

## Independence vs comfort (product fork)

Google Wallet is a **licensed front-end** onto card networks. “Same tap comfort
without Google” means switching the **issuer app**, not forking Wallet:

| Comfort level | Approach |
| ------------- | -------- |
| Max comfort, accept Google | Stock or near-stock Android + Wallet (custom ROM often breaks Wallet) |
| Less Google, keep tap-to-pay | Custom Android + **bank / Curve / PayPal-class** wallet that works without Google Pay; verify on device |
| Strong Google independence | Custom Android or Linux; tap-to-pay via physical card/watch; no Wallet clone |

**If Google Wallet itself is non-negotiable**, building Neodroid far from GMS
is low value — stay on stock or a ROM that still passes Wallet’s checks (rare).
**If “tap with *a* phone wallet” is enough**, independence remains viable on
custom Android with the right bank/third-party app.

## Open-source NFC wallets — what exists

| Kind | Examples | Pays at Visa/MC shop terminal? |
| ---- | -------- | ------------------------------ |
| **FOSS Google Wallet replacement (EMV card pay)** | — | **None known / practical** — needs scheme license + secrets, not just an APK |
| **FOSS HCE demos / closed-loop** | Android HCE samples, festival cashless (Fedow/TiBillet) | Only on **that** network’s readers |
| **FOSS crypto / ecash NFC** | Cashu **Numo** (merchant POS via NDEF), Village Wallet–class NFC crypto cards | Only where the other side runs the same stack |
| **FOSS NFC utilities** | Tag readers/writers, access-card tools | Not payment |
| **Open wallet standards (identity / credentials)** | OpenWallet Foundation, walt.id-class | Credentials / future wallets — **not** today’s EMV tap |

So: **yes, FOSS NFC “wallets” exist**, but they are **not** drop-in EMV card wallets.
“Compatible NFC” ≠ “works on every merchant terminal.”

## “Open-source bank” vs merchant NFC

**No open-source bank replaces Visa/Mastercard at the shop terminal.** Two layers:

| Layer | What exists | Accepted at random shops? |
| ----- | ----------- | ------------------------- |
| **Core banking software** (ledgers, accounts) | Apache Fineract / Mifos, FinAegis, Midaz (source-available), etc. | N/A — software only; still needs a licensed PSP / scheme to hit real money rails |
| **Card schemes / EMV tap** | Visa, Mastercard, Amex, regional debit schemes | Yes — closed membership, certification, not FOSS |
| **Account-to-account rails** | SEPA Instant (EU), Pix, UPI, … | At merchants that support **QR / request-to-pay**, not classic EMV NFC |
| **Open building blocks on open rails** | e.g. EUPI (SEPA Instant QR libs), GNU Taler | Growing; still need a regulated PSP; not a drop-in Wallet |
| **Local / complementary cashless** | Fedow + TiBillet (NFC cards for festivals, MLCC) | Only where that federation is deployed |

Implication for Neodroid: **independence from international card schemes** means
accepting a **different UX** (QR SEPA Instant, bank app, cash, physical card) —
not an FOSS bank that taps the same terminals as Visa. Building or joining such
a bank/PSP is a **fintech/regulatory project**, orders of magnitude beyond a
phone OS.

## Mechanisms (Android)

- **HCE** (Host Card Emulation): app emulates a payment AID; needs a cooperating
  wallet/bank app, not a dump of the plastic card.
- **Secure Element / off-host**: OEM/vendor TEE paths; often tied to stock OS.
- Google Wallet additionally requires Google’s certification stack — fails on
  most custom ROMs even when NFC hardware works.

## Implications for Neodroid routes

| Stack | NFC payment outlook |
| ----- | ------------------- |
| Custom Android (Lineage-class, no GMS) | Hardware NFC can work; payment depends on **specific apps** that tolerate unlocked bootloaders / missing attestation |
| Custom Android + sandboxed Play (Graphene-like) | Better app compatibility; Google Wallet still often blocked |
| Linux + Waydroid | Poor NFC bridge → treat tap-to-pay as **unsupported** unless proven on target device |
| Mobile NixOS | Same as Linux path unless a native Linux payment stack appears (none mainstream) |

## Product options (to decide later)

1. **Must-have NFC pay** → bias toward **Android custom ROM** + verify the
   user's bank/wallet app on a candidate device early.
2. **Nice-to-have** → document fallbacks (physical card, watch, bank-specific
   app) and do not block v0.
3. **Explicit non-goal** → record in [[../features/out-of-scope|out-of-scope]]
   if declined.

## Action before locking the stack

- List the user's current payment method (Google Wallet vs bank app vs Curve-like).
- On a candidate unlocked device, test that payment app on a close ROM (e.g.
  Lineage/Graphene for that model) **before** investing in Linux/Nix ports.

## References

- Waydroid NFC discussion: https://github.com/waydroid/waydroid/issues/980
- GrapheneOS community: NFC works; Google Wallet does not; alternatives exist
- Android HCE docs (platform frameworks)
- Example write-up: contactless payments on GrapheneOS via Curve (UK, 2025)
