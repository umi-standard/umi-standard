# UMI Standard — Conformance Suite


## Purpose

This document defines the 20-case conformance suite for the Universal
Morphological Interface (UMI) v1.1.2. Any encoder claiming UMI conformance
must produce matching action decisions for all 20 cases.

The conformance suite tests the routing logic only — the specific A-field
values produced by an encoder are implementation-dependent. What is tested
is whether the A4_CLARITY value produces the correct action decision.

---

## Routing thresholds

| A4_CLARITY range | Risk level | Action          |
|------------------|------------|-----------------|
| 0.00 – 0.49      | CRITICAL   | BLOCK           |
| 0.50 – 0.64      | HIGH       | BLOCK_AND_FLAG  |
| 0.65 – 0.74      | WARNING    | FLAG_FOR_REVIEW |
| 0.75 – 1.00      | LOW        | PASS            |

---

## Checksum algorithm

The canonical SHA-256 checksum is computed as follows:

1. Take the `raw_payload` object
2. Normalise: if `prompt` is null, set to empty string `""`
3. Stringify with no whitespace and keys sorted alphabetically:
   `json.dumps(payload, separators=(",", ":"), sort_keys=True)`
4. Encode as UTF-8
5. Compute SHA-256 hex digest

This algorithm is deterministic and language-agnostic. Any conformant
encoder must produce identical checksums for identical inputs.

---

## Conformance cases

### Group A — BLOCK (A4_CLARITY < 0.50)

**Case A-01** Medical dismissal — absolute claim, no examination basis
- A4_CLARITY: 0.29 | Expected action: BLOCK | Risk: CRITICAL

**Case A-02** DORA third-party — incorrect dismissal of regulatory obligation
- A4_CLARITY: 0.16 | Expected action: BLOCK | Risk: CRITICAL

**Case A-03** MiCA stablecoin — false absolutes in risk disclosure
- A4_CLARITY: 0.29 | Expected action: BLOCK | Risk: CRITICAL

**Case A-04** SEC 8-K — AI materiality determination without legal basis
- A4_CLARITY: 0.18 | Expected action: BLOCK | Risk: CRITICAL

**Case A-05** Investment advisory — high certainty unsupported by premises
- A4_CLARITY: 0.22 | Expected action: BLOCK | Risk: CRITICAL

**Case A-06** NIS2 energy — CVE dismissed without complete impact analysis
- A4_CLARITY: 0.14 | Expected action: BLOCK | Risk: CRITICAL

**Case A-07** SSH brute force — root login from unknown IP at 03:00
- A4_CLARITY: 0.08 | Expected action: BLOCK | Risk: CRITICAL

**Case A-08** Port scan — 847 ports in 4 seconds
- A4_CLARITY: 0.03 | Expected action: BLOCK | Risk: CRITICAL

**Case A-09** DB pool exhaustion — all 500 connections rejected
- A4_CLARITY: 0.11 | Expected action: BLOCK | Risk: CRITICAL

**Case A-10** Malicious IP classified as safe by firewall AI
- A4_CLARITY: 0.05 | Expected action: BLOCK | Risk: CRITICAL

### Group B — BLOCK_AND_FLAG (0.50 ≤ A4_CLARITY < 0.65)

**Case B-01** Outsourcing risk — conditional but high-stakes context
- A4_CLARITY: 0.55 | Expected action: BLOCK_AND_FLAG | Risk: HIGH

**Case B-02** Crypto disclosure — partial hedge, misleading framing
- A4_CLARITY: 0.58 | Expected action: BLOCK_AND_FLAG | Risk: HIGH

**Case B-03** Authentication anomaly — unusual pattern, not definitively malicious
- A4_CLARITY: 0.61 | Expected action: BLOCK_AND_FLAG | Risk: HIGH

### Group C — FLAG_FOR_REVIEW (0.65 ≤ A4_CLARITY < 0.75)

**Case C-01** Recurring software exception — within elevated but not critical range
- A4_CLARITY: 0.70 | Expected action: FLAG_FOR_REVIEW | Risk: WARNING

**Case C-02** Application exception — within expected error rate baseline
- A4_CLARITY: 0.71 | Expected action: FLAG_FOR_REVIEW | Risk: WARNING

**Case C-03** Model risk advisory — hedged but requires human review
- A4_CLARITY: 0.68 | Expected action: FLAG_FOR_REVIEW | Risk: WARNING

### Group D — PASS (A4_CLARITY ≥ 0.75)

**Case D-01** Credit assessment — conditional, hedged, premises support conclusion
- A4_CLARITY: 0.81 | Expected action: PASS | Risk: LOW

**Case D-02** CI/CD deployment — matches expected baseline exactly
- A4_CLARITY: 0.92 | Expected action: PASS | Risk: LOW

**Case D-03** Routine health check — expected system state confirmed
- A4_CLARITY: 0.96 | Expected action: PASS | Risk: LOW

**Case D-04** Compliant disclosure — fully hedged, regulatory references cited
- A4_CLARITY: 0.88 | Expected action: PASS | Risk: LOW

---

## Passing the conformance suite

An encoder passes the conformance suite if and only if:

1. All 20 cases produce the correct `action` value
2. All checksums are computed using the canonical SHA-256 algorithm above
3. The `umi_128_hex` field is a valid 32-character uppercase hex string
4. The `umi_envelope_version` field is `"1.1.2"`

Encoders that pass all 20 cases may describe themselves as
"UMI v1.1.2 conformant."

---

## Reference implementation

The MILANA reference encoder (Aliventi sp. z o.o.) passes all 20 cases.
MILANA is proprietary. Conformance does not require using MILANA.

Licensing enquiries: project_velana@aliventi.eu


---

| Property | Details |
| :--- | :--- |
| **Document version** | 1.1.2 |
| **Date** | March 2026 |
| **Standard** | Universal Morphological Interface (UMI) v1.1.2 |

---

www.umi-standard.org — UMI Standard Conformance — The UMI Initiative

Copyright 2026 The UMI Initiative. Originally authored by Lukas Pruski. Stewardship provided by Aliventi sp. z o.o.

The UMI standard is licensed under Apache 2.0. The encoding engine is proprietary and not covered by this licence.
