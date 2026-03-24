# UMI Initiative — Governance

## Structure

```
UMI-STANDARD
  └── maintained by the UMI Initiative
        └── stewardship currently provided by Aliventi sp. z o.o.
              └── originally authored by Lukas Pruski
```

---

## What the UMI Initiative is

The UMI Initiative is not a legal entity. It is a project-level
stewardship construct used to separate the standard from any single
commercial product or organisation.

Its purpose is to provide a neutral, named home for the UMI standard —
one that makes clear that UMI-STANDARD exists as an independent
specification, regardless of which organisations build implementations
on top of it.

---

## Current stewardship

The UMI Initiative is currently operated with stewardship provided by
**Aliventi sp. z o.o.**, a technology company registered in Poland.

The UMI standard was originally authored by **Lukas Pruski**, who serves
as author, chief architect, and primary maintainer. Authorship is dated
to October 2025, with public release of v1.1.2 in March 2026.

At this stage, technical direction and schema changes are led by the
original author within the UMI Initiative, with openness to external
contribution as the project evolves.

---

## Relationship to commercial implementations

The UMI Initiative governs the standard only. It does not govern,
endorse, or control any commercial implementation built on the standard.

MILANA Lite — the reference encoder for UMI — is a proprietary product
developed and maintained by Aliventi sp. z o.o. It is one conformant
implementation among potentially many. Its development roadmap,
licensing, and commercial terms are entirely separate from this
governance document.

The same applies to AiQUS, VELANA, and any other product that references
or implements UMI. Building on UMI does not confer governance rights,
and governance rights do not imply commercial relationship.

Licensing enquiries for proprietary implementations:
project_velana@aliventi.eu

---

## Contribution model

The UMI standard is published under the Apache License 2.0.
Contributions are welcome.

**What can be contributed via pull request:**
- Corrections to documentation and regulatory reference descriptions
- New example records demonstrating conformant encoder output
- Additional conformance test cases with documented rationale
- Translations of documentation

**What requires steward review and explicit approval:**
- Changes to `umi.schema.json`
- Changes to `regulatory_flags.enum.json` or any `flags/` file
- Changes to the 128-bit cluster specification in README.md
- Changes to CONFORMANCE.md routing thresholds or test cases
- Any change that affects backwards compatibility

**Conformant encoder submissions:**
Any organisation that builds a conformant UMI encoder may submit a pull
request to be listed as a conformant implementation. See CONFORMANCE.md
for validation requirements.

---

## Future governance

The UMI Initiative is a transitional construct, not a permanent structure.

If and when external adoption and contribution justify it, stewardship
may transition to a more formal governance structure. No such structure
is currently defined or promised.

The decision to transition, and the form that transition takes, will be
made transparently and documented here.

---

## Contact

Standard enquiries: raise a GitHub issue or pull request at
github.com/umi-standard/umi-standard

Commercial and API enquiries: project_velana@aliventi.eu


---

| Property | Details |
| :--- | :--- |
| **Document version** | 1.1.2 |
| **Date** | March 2026 |
| **Standard** | Universal Morphological Interface (UMI) v1.1.2 |

---

www.umi-standard.org — UMI Standard Governance — The UMI Initiative

Copyright 2026 The UMI Initiative. Originally authored by Lukas Pruski. Stewardship provided by Aliventi sp. z o.o.

The UMI standard is licensed under Apache 2.0. The encoding engine is proprietary and not covered by this licence.
