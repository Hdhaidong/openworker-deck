# Any-Agent Architecture — Three Compute Layers, One Hardware Boundary

> OpenWorker Deck technical note · design-stage (EVT targets) · part of the [hardware binding spec](https://github.com/andrewyng/openworker/pull/596) track

中文摘要见 [README](../README.md#换大脑不换身体--grok-ready-定制版)。

## The invariant

Three compute layers answer one question — *where the compute happens*. They never change where the boundary lives:

| Rule | Meaning |
|---|---|
| **gate** | The mandatory authorization gate is the only path to any cloud model. No bypass, no direct API, no debug backdoor. |
| **write** | Any agent device-write passes the physical Approve button. However large the cloud compute, it goes through this button. |
| **return** | Cloud responses are signed and land back on the local encrypted cartridge. Nothing is retained in the cloud. |
| **wallet** | Compute credits are deducted offline inside the cartridge's secure element. The cloud sees "this card authorized this call" — never the balance or the identity behind it. |
| **never** | Raw data, personal baselines, key material — never leave the cartridge, on any layer. |

## Layer 1 — On-device NPU sandbox (first priority)

The only layer with zero third-party dependencies. If every partner disappears tomorrow, the product is still complete.

- **Host**: Home Hub / desk / DIN-rail boards, NPU module seated on the EVT PCB (see [pcb-design.md](../hardware/pcb-design.md))
- **Models**: a sub-4B SLM (INT4) plus a purpose-built anomaly detector (current signature + per-machine baseline)
- **Resident duties** — hardcoded read-only in firmware, never offloaded: personal baselines · anomaly detection · weather math · risk briefs
- **Offline**: full night-shift loop works with the network unplugged. EVT acceptance hard-gates on this.

## Layer 2 — Cloud supercompute through the gate (Grok-ready editions)

For large-model inference beyond on-device capacity. The calling discipline:

1. Consent card present, and its declared fields cover this request
2. Physical Approve pressed within the session
3. Request carries **aggregated features only** — never raw time-series
4. Response lands on the cartridge with a device signature (model ID · token count · timestamp · card ID)
5. Every deduction writes an audit record, paired one-to-one with the call

The API key lives inside the cartridge's secure element — zero plaintext keys in device firmware. Swapping cards swaps identity; multiple vendor keys can coexist. If the endpoint is unreachable, the call degrades silently to Layer 1 and the task continues.

Provider-agnostic by design: xAI today, any compatible endpoint tomorrow. "Grok-ready" refers to protocol compatibility only — no affiliation with or endorsement by xAI.

## Layer 3 — Satellite backhaul

For sites with no ground network (rangeland, pump stations, valleys): LoRa near-field aggregation at the node → gateway uplink via satellite (Starlink-class service). Same software path is validated on 4G Cat-1 during EVT. The industrial SKU keeps an external antenna port and redundant PoE input. We integrate nothing and resell nothing — users bring their own terminal and subscription. This layer is detachable: without it, Layer 2 runs on ground networks and the product remains complete.

## Compute-credit cold wallet

The same floppy-form encrypted cartridge stores both data and prepaid compute credit:

- **Balance** lives in the secure element — cold storage, offline-readable, atomic deduction, double-spend impossible
- **Pricing** is per token, denominated at a USDT-pegged rate
- **Refill** uses one-time signed voucher codes confirmed at the Approve button; a gift card is a physical voucher — give the card, give the compute
- **Every deduction** produces a signed receipt: caller · model · token count · amount · remaining balance

Compliance posture, stated plainly: the card stores a credit number only. No token is issued, nothing goes on-chain, the balance earns no yield and never appreciates. It is a prepaid meter, not a wealth-management product. Single-purpose (spendable only on this product's cloud inference), no expiry, per-card prepaid cap, records retained five years.

## Engineering milestones

Design freeze (now) → EVT (~10 weeks) → DVT (~8 weeks) → PVT & certification (~6 weeks) → production (~8 weeks).

EVT acceptance, layer by layer:

| # | Check | Pass condition |
|---|---|---|
| V1 | Offline night-shift loop | 8 h unplugged: sense → infer → store → write, full function |
| V2 | Signed call chain | Any cloud call resolvable to the five-field audit tuple |
| V3 | No-consent refusal | Card pulled → every cloud call attempt fails immediately, no bypass |
| V4 | Double-spend | Two concurrent deductions → balance decrements once |
| V5 | Balance migration | Card moved to another device → balance and audit intact |
| V6 | Brain swap | Agent image reflashed on the same unit → MHS binding succeeds, hardware untouched |
| V7 | API degradation | Endpoint down → task continues in local mode, UI labels it |
| V8 | Compliance copy | All public materials match the frozen wording — no token / no chain / no yield |

## Export control

The encrypted cartridge and secure element are controlled items: embargoed destinations never ship (Belarus, Cuba, Iran, North Korea, Russia, Sudan, Syria, disputed regions of Ukraine); second-tier destinations require import-side licensing first; mass-market path elsewhere (US 5A992.c self-classification with annual self-report; China Cryptography Law consumer exemption; Hong Kong mass-market exemption).

---

*OpenWorker Deck is an independent community project — not affiliated with, endorsed by, or connected to the OpenWorker project or xAI. Grok and Starlink are trademarks of their respective owners.*
