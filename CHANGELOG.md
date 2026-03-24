# UMI Standard — Changelog


All notable changes to the UMI schema, conformance suite, and
regulatory flag enumeration are documented here.

Format: [VERSION] — DATE — description

---

## [1.1.2] — 2026-03-24 — Public contribution release

### Added
- GOVERNANCE.md — stewardship model, contribution process, entity separation
- REGULATORY_REFERENCE.md — full descriptions of all 47 flags
- `EU_CYBER_RESILIENCE_ACT` flag — Cyber Resilience Act product security
- `EU_EIDAS2_TRUST_SERVICE` flag — eIDAS 2.0 qualified trust services
- `DE_BSI_C5_CLOUD_AUDIT` flag — BSI C5 cloud compliance audit
- SIEM example records — `dora_db_connection_exhaustion_block.json`,
  `nis2_ssh_brute_force_block.json`
- `generate_examples.py` — canonical example generator with self-validation
- `generate_regulatory_flags.py` — jurisdiction enum generator with validation
- `DEMO_AUDIT_ENGINE_v2.py` — heuristic demonstration engine (not conformant)

### Changed
- Schema version field updated to `1.1.2`
- All `$comment` attribution updated to UMI Initiative / Aliventi stewardship
- Conformance suite expanded to 20 cases (Groups A–D)

### Fixed
- Checksum algorithm documented in CONFORMANCE.md
- Version consistency across all JSON files verified

---

## [1.1.0] — 2026-02-15 — Multi-jurisdiction expansion

### Added
- Australia jurisdiction flags (5): APRA CPS230, CPG234, OAIC, ASIC RG273, ASD Essential Eight
- Canada jurisdiction flags (5): AIDA, PIPEDA, OSFI B-10, OSFI E-23
- `flags/` subdirectory with per-jurisdiction enum files
- `aida_apra_investment_block.json` example record
- `sec_8k_materiality_block.json` example record

### Changed
- Total flags: 32 → 44
- Jurisdictions: 4 → 6

---

## [1.0.0] — 2025-10-01 — Initial release

### Added
- `umi.schema.json` — core envelope schema
- `regulatory_flags.enum.json` — 32 flags across EU, DE, UK, US
- `CONFORMANCE.md` — initial 12-case conformance suite
- Example records: `eu_ai_act_medical_block.json`,
  `eu_ai_act_credit_pass.json`, `nis2_energy_critical.json`,
  `mica_stablecoin_disclosure.json`, `CANONICAL_FORMAT_REFERENCE.json`
- `LICENSE` — Apache 2.0 with proprietary carve-out
- `README.md` — standard overview and quick start

### Architecture decisions recorded
- 128-bit fixed-width envelope chosen for database index compatibility
- Five A-fields (A1–A5) chosen as minimum sufficient extraction set
- A4_CLARITY as primary routing metric — single tunable threshold
- SHA-256 canonical checksum for tamper-evidence
- `context_metadata` as substrate extension point (no schema changes required)


---

| Property | Details |
| :--- | :--- |
| **Document version** | 1.1.2 |
| **Date** | March 2026 |
| **Standard** | Universal Morphological Interface (UMI) v1.1.2 |

---

www.umi-standard.org — UMI Standard Changelog — The UMI Initiative

Copyright 2026 The UMI Initiative
Originally authored by Lukas Pruski
Stewardship provided by Aliventi sp. z o.o.

The UMI standard is licensed under Apache 2.0.
The encoding engine is proprietary and not covered by this licence.
