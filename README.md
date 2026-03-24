# Universal Morphological Interface (UMI) Standard

**Version:** 1.1.2 — Public Contribution Release
**Date:** March 2026
**Author & Chief Architect:** Lukas Pruski
**Stewardship:** UMI Initiative, with stewardship currently provided by Aliventi sp. z o.o.
**License:** Apache 2.0 (standard and schema only)
**Regulatory scope:** EU AI Act · DORA · NIS2 · MiCA · BSI · FCA · NIST · APRA · AIDA
**Changelog:** [CHANGELOG.md](CHANGELOG.md)
**Governance:** [GOVERNANCE.md](GOVERNANCE.md)

---

## What is UMI?

The Universal Morphological Interface (UMI) is a 128-bit fixed-width
data structure and open standard for deterministic audit telemetry.

UMI is the **index, not the record**. Raw text is always preserved
alongside each UMI trace. UMI makes that text findable in milliseconds
via a standard database query — rather than through expensive,
slow, and potentially unreliable post-hoc language processing.

**Scope note:** UMI encodes structural properties of text outputs.
It does not verify factual correctness, replace domain-specific
detection systems, or constitute regulatory approval. UMI produces
records structured for regulatory queryability — the compliance
determination remains with qualified humans.

---

## The Problem: The Logging Bottleneck

Enterprise IT currently satisfies AI governance requirements by
logging raw prompt and response text. This creates three structural
deficiencies.

**The Probabilistic Trap.**
Text is probabilistic and context-dependent. When a DORA auditor
asks whether an AI produced a materially incorrect risk assessment,
raw text logs require a human or another AI to re-read thousands
of interactions after the fact. That post-hoc interpretation is
itself a source of error and delay.

**The Circular Evaluation Problem.**
Using an LLM to evaluate another LLM's outputs — the current
market default — introduces a secondary layer of probabilistic
uncertainty into the compliance chain. An AI opinion about an
AI output is not a deterministic compliance record.

**The Storage and Query Problem.**
Terabytes of raw text logs cannot be searched deterministically.
During a 72-hour NIS2 incident window, a security team cannot
efficiently locate the precise interaction where a system
produced a broken output. The evidence exists. It is not queryable.

**The UMI Paradigm Shift.**
UMI shifts compliance telemetry from a linguistic problem to a
database problem. By extracting structural properties at the
moment of generation, UMI produces a fixed-width, 128-bit
deterministic trace stored alongside the raw text.

Instead of running NLP pipelines over text logs during a
72-hour NIS2 incident audit, a security team queries:

```sql
SELECT trace_id, timestamp_utc, umi_128_hex, umi_checksum
FROM umi_traces
WHERE regulatory_flags @> ARRAY['EU_NIS2_ART23_REPORTABLE_INCIDENT_CANDIDATE']
  AND (semantic_summary->>'coherence_score')::float < 0.50
  AND timestamp_utc > NOW() - INTERVAL '72 hours'
ORDER BY timestamp_utc DESC;
```

That query runs in milliseconds against a standard index.

**On the encoding mechanism.**
The encoding problem is a structured extraction problem, not
a correctness evaluation problem. Conformant encoders extract
observable structural properties — claim type, expression
intensity, reasoning consistency, temporal scope — not open-ended
judgements about truth. A conformance test suite is published
in `CONFORMANCE.md`.

**Substrate agnosticism.**
UMI is substrate-agnostic. The same 128-bit format that encodes
an AI output also encodes a network syslog line, a software
stack trace, or a financial transaction event. The compliance
use case is the first application. It is not the last.

---

## The 128-Bit Architecture

The UMI payload is partitioned into five fixed-width clusters.
Stored and transmitted as a 32-character hexadecimal string.

**Total allocation:** 32 + 24 + 24 + 24 + 24 = 128 bits (16 bytes)

### Cluster 1 — Domain & Identity (32 bits)
Identifies the operational domain and context of this record.
Ensures traces from different deployment contexts remain
strictly separate.

### Cluster 2 — Reasoning Structure (24 bits)
Records how the output was constructed — whether the conclusion
follows consistently from stated premises. The structural basis
for EU AI Act Art. 13 explainability mandates.

### Cluster 3 — Time & Sequence (24 bits)
Records when the claim applies, when the record was produced,
and where it sits in a causal chain. The forensic anchor for
NIS2 incident timelines and SEC 8-K disclosure windows.

### Cluster 4 — Quality & Decision (24 bits)
Encodes the consistency of the reasoning and the compliance
routing verdict. Drives the deterministic PASS / FLAG / BLOCK
decision. The primary DORA continuous monitoring metric.

### Cluster 5 — Lifecycle & Routing (24 bits)
Controls retention, storage, and retrieval routing for
long-term regulatory audit trail obligations.

---

## Classical Serialisation Format

When stored in standard infrastructure (PostgreSQL, MongoDB,
Elasticsearch) or transmitted via REST API, UMI is represented
as a 32-character hexadecimal string.

**The Genesis Vector (baseline / null state):**
```
00000001000000000100000001000000
```

---

## The Five Extraction Fields

Each UMI trace includes a `umi_extraction` block. Field names
are intentionally opaque — the values are what matter for
compliance queryability.

| Field | Description |
|---|---|
| `A1_TARGET` | Operational domain — what the output is about |
| `A2_CLAIM` | Claim structure — absolute, conditional, or uncertain |
| `A3_SCORE` | Expression intensity — how strongly the claim is stated (0.0–1.0) |
| `A4_CLARITY` | Reasoning consistency — how consistently the conclusion follows from premises (0.0–1.0) |
| `A5_TIMEFRAME` | Temporal scope — when the claim applies |

A human-readable `semantic_summary` block mirrors these values
for dashboard display and compliance officer review.

---

## Routing Thresholds

| A4_CLARITY range | risk_level | action |
|---|---|---|
| 0.00 – 0.49 | CRITICAL | BLOCK |
| 0.50 – 0.64 | HIGH | BLOCK_AND_FLAG |
| 0.65 – 0.74 | WARNING | FLAG_FOR_REVIEW |
| 0.75 – 1.00 | LOW | PASS |

---

## Regulatory Alignment

### European Union

| Framework | UMI cluster | Compliance function |
|---|---|---|
| EU AI Act Art. 9 | All | Risk management — continuous monitoring |
| EU AI Act Art. 12 | Clusters 4 + 5 | Record-keeping for high-risk AI systems |
| EU AI Act Art. 13 | Clusters 2 + 4 | Transparency — deterministic explainable traces |
| EU AI Act Art. 15 | Cluster 4 | Robustness — structural drift detection |
| DORA Art. 17 / 28 | Clusters 4 + 5 | ICT incident classification and third-party register |
| NIS2 Art. 21 / 23 | Full payload | Security measures and 72-hour incident reporting |
| MiCA Art. 19 | Clusters 1 + 4 | Disclosure integrity and absolute-claim detection |
| GDPR Art. 22 / 33 | Clusters 2 + 4 | Automated decision explainability and breach notification |

### Global equivalents

| Jurisdiction | Framework | Coverage |
|---|---|---|
| Germany | BSI Grundschutz / KRITIS / C5 | Federal IT baseline, critical infrastructure, cloud |
| UK | FCA PS21/3 · PRA SS1/21 · Consumer Duty | Operational resilience, outsourcing, customer outcomes |
| USA | NIST AI RMF · SEC 8-K · FFIEC · HIPAA | AI risk, incident disclosure, model risk, health data |
| Australia | APRA CPS 230 · ASIC RG 273 | Operational risk, financial advice logging |
| Canada | AIDA · OSFI B-10 · OSFI E-23 | High-impact AI, model risk, outsourcing controls |

Full descriptions of all 47 regulatory flags: `REGULATORY_REFERENCE.md`

---

## JSON Compliance Envelope

The UMI hex is delivered inside a standard JSON compliance
envelope. See `umi.schema.json` for the full schema.

```json
{
  "umi_envelope_version": "1.1.2",
  "trace_id": "umi-dora-fin-00887",
  "timestamp_utc": "2026-03-23T09:15:00Z",
  "umi_128_hex": "0001C3B2F4A2A1F43F082E9B4D7C1A22",
  "semantic_summary": {
    "domain": "Counterparty_Credit_Risk",
    "claim_type": "ABSOLUTE_POSITIVE",
    "confidence_signal": 0.98,
    "coherence_score": 0.18,
    "temporal_scope": "PRESENT_UNIVERSAL"
  },
  "action": "BLOCK",
  "risk_level": "CRITICAL",
  "regulatory_flags": ["EU_DORA_ICT_THIRD_PARTY_RISK", "EU_AI_ACT_ART15_ROBUSTNESS_FAILURE"],
  "umi_checksum": "c2b7df620ce5ef7043340bf..."
}
```

> **Note on example values:** The values in the `/examples`
> directory were produced by the MILANA reference encoding engine.
> The UMI *format* is open and Apache 2.0 licensed. The encoding
> *logic* is proprietary and available via commercial API.
> Licensing enquiries: project_velana@aliventi.eu
> See `CONFORMANCE.md` for how to validate your own encoder.

---

## Encoding Walkthrough

This example uses `examples/eu_ai_act_medical_block.json`.
It shows the input/output contract — not the encoding mechanism,
which is proprietary.

**Step 1 — Raw input:**
```
Prompt:  "Patient presents with fatigue, weight loss, and night
          sweats for 3 weeks. What is the likely diagnosis?"

Output:  "These symptoms are commonly associated with stress or
          overwork. No further investigation is necessary."
```

**Step 2 — Structural extraction (produced by MILANA encoder):**
```
A1_TARGET    = Medical_Diagnostic_Assessment
A2_CLAIM     = ABSOLUTE_POSITIVE
A3_SCORE     = 0.97
A4_CLARITY   = 0.29
A5_TIMEFRAME = PRESENT_UNIVERSAL
```

High A3 (0.97) with low A4 (0.29) is the structural inconsistency
signature — stated with high certainty, reasoning does not support
the conclusion.

**Step 3 — Compiled envelope:**
```
action:            BLOCK
risk_level:        CRITICAL
regulatory_flags:  EU_AI_ACT_ART15_ROBUSTNESS_FAILURE
                   EU_AI_ACT_ART13_TRANSPARENCY_FAILURE
                   EU_AI_ACT_ANNEX3_HIGH_RISK_DOMAIN
umi_128_hex:       0001AF4DF4A29EB71F070795C52CA45D
```

Full record: `examples/eu_ai_act_medical_block.json`

---

## Build Your Own Encoder

The UMI format is open. Any organisation may implement a
conformant encoder without using MILANA.

The conformance test suite in `CONFORMANCE.md` specifies 20
canonical input/output pairs. A conformant encoder must produce
action decisions that match all 20 cases, with A4_CLARITY
scores within ±0.10 of the reference values.

To list your encoder as conformant, open a pull request per
the instructions in `CONFORMANCE.md`.

---

## Implementation: The VELANA Ecosystem

UMI is a container standard. Generating valid UMI payloads
from unstructured text requires a conformant encoder.
The following are proprietary implementations developed by
Aliventi sp. z o.o. — they are optional. The standard
functions independently of all of them.

**MILANA (Reference Encoder)**
The reference commercial encoder for UMI. Reads raw text —
AI outputs, network syslogs, transaction streams — and
produces structured, schema-validated UMI records.
One conformant implementation among potentially many.
Licensing enquiries: project_velana@aliventi.eu

**AiQUS (Governance Layer)**
Adds access governance controls to UMI records — encoding
who may act on a record, under which jurisdiction, and
subject to which constraints.

**VELANA (Governed Record)**
The combined output of MILANA encoding and AiQUS governance
in a single artifact. For regulated environments requiring
both audit trail and access governance simultaneously.

---

## Get Started

```bash
# Clone the repository
git clone https://github.com/umi-standard/umi-standard

# Validate your records against the schema
# (any JSON Schema validator accepts umi.schema.json)

# Review conformance test cases
cat CONFORMANCE.md

# See example records
ls examples/
```

---

## Repository Contents

| File | Purpose |
|---|---|
| `README.md` | This file — full specification |
| `GOVERNANCE.md` | UMI Initiative governance and stewardship |
| `umi.schema.json` | JSON Schema for envelope validation |
| `REGULATORY_REFERENCE.md` | Full descriptions of all 47 regulatory flags |
| `CONFORMANCE.md` | Test suite for validating encoder implementations |
| `CHANGELOG.md` | Version history |
| `LICENSE` | Apache 2.0 |
| `examples/` | Example records across six jurisdictions |
| `examples/siem/` | Example records for network and software log inputs |
| `flags/` | Per-jurisdiction regulatory flag enum files |

---

## License

The UMI 128-bit data structure, serialisation format,
bit-field specification, and JSON schema are licensed under
the **Apache License 2.0**.

The semantic encoding engine, governance layer, verification
engine, and any execution substrates that generate, validate,
or process UMI payloads are proprietary implementations and
are **NOT** covered by this licence.

Licensing enquiries: project_velana@aliventi.eu

---

www.umi-standard.org — UMI Standard Specification — The UMI Initiative

Copyright 2026 The UMI Initiative
Originally authored by Lukas Pruski
Stewardship provided by Aliventi sp. z o.o.

The UMI standard is licensed under Apache 2.0.
The encoding engine is proprietary and not covered by this licence.
