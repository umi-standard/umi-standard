# UMI Standard — Regulatory Reference


Canonical descriptions of all 47 regulatory flags across 6 jurisdictions.
Use this file to understand which flag applies to which regulatory obligation.

---

## European Union (20 flags)

### EU AI Act

**EU_AI_ACT_ART9_RISK_MANAGEMENT**
Art. 9 — Risk management system requirement for high-risk AI systems.
Triggered when a UMI record indicates the AI system lacks adequate risk
management documentation or process.

**EU_AI_ACT_ART12_LOGGING**
Art. 12 — Logging requirements for high-risk AI systems.
Triggered when logging is absent or insufficient for the interaction type.

**EU_AI_ACT_ART13_TRANSPARENCY_FAILURE**
Art. 13 — Transparency and provision of information to users.
Triggered when an AI output makes absolute claims without disclosing
uncertainty, limitations, or the AI nature of the output.

**EU_AI_ACT_ART15_ROBUSTNESS_FAILURE**
Art. 15 — Accuracy, robustness, and cybersecurity.
Triggered when A4_CLARITY falls below 0.50 in a high-risk domain,
indicating the output does not meet robustness requirements.

**EU_AI_ACT_ANNEX3_HIGH_RISK_DOMAIN**
Annex III — High-risk AI system domain classification.
Triggered when A1_TARGET maps to a domain listed in Annex III:
biometric identification, critical infrastructure, education, employment,
essential services, law enforcement, migration, justice, democratic processes.

### DORA

**EU_DORA_ICT_THIRD_PARTY_RISK**
Art. 28 — ICT third-party risk management.
Triggered when an AI output incorrectly assesses or dismisses obligations
arising from use of third-party ICT service providers.

**EU_DORA_ART17_MAJOR_INCIDENT**
Art. 17 — ICT-related incident classification.
Triggered when A4_CLARITY falls below 0.50 in an ICT operational context,
indicating a potential major ICT incident requiring classification.

**EU_DORA_ART28_THIRD_PARTY_REGISTER**
Art. 28 — Third-party ICT provider register.
Triggered when an AI output produces incorrect guidance about third-party
ICT register obligations. Paired with EU_DORA_ICT_THIRD_PARTY_RISK.

**EU_DORA_COMPLIANCE_RISK**
General DORA compliance risk indicator.
Triggered when the interaction context involves DORA-regulated entities
and the output contains structural inconsistencies.

### NIS2

**EU_NIS2_ART21_INADEQUATE_RISK_ASSESSMENT**
Art. 21 — Cybersecurity risk management measures.
Triggered when an AI output dismisses or inadequately assesses a
cybersecurity risk for an essential or important entity.

**EU_NIS2_ART23_REPORTABLE_INCIDENT_CANDIDATE**
Art. 23 — Reporting obligations — 72-hour early warning.
Triggered when the UMI record documents an event that may meet the
threshold for NIS2 incident reporting. The UMI trace serves as the
forensic receipt for the reporting chain.

**EU_NIS2_FORENSIC_RECORD**
NIS2 forensic record indicator.
Indicates this UMI trace is being retained as part of the NIS2
incident documentation chain. Complements ART23 flag.

### MiCA

**EU_MICA_ART19_MISLEADING_CONTENT**
Art. 19 — Marketing communications for crypto-assets.
Triggered when an AI output contains misleading claims about
crypto-asset characteristics, risks, or returns.

**EU_MICA_FALSE_ABSOLUTE_CLAIM**
MiCA false absolute claim indicator.
Triggered when ABSOLUTE_POSITIVE claim type is combined with
low A4_CLARITY in a crypto-asset disclosure context.

**EU_MICA_MARKET_INTEGRITY_RISK**
MiCA market integrity risk indicator.
Triggered when output may constitute market manipulation or
misleading information under MiCA Title VI.

### GDPR

**EU_GDPR_ART22_AUTOMATED_DECISION**
Art. 22 — Automated individual decision-making.
Triggered when an AI output constitutes or influences an automated
decision with legal or similarly significant effects on individuals.
This UMI record is the Art. 22 audit trail.

**EU_GDPR_ART33_BREACH_NOTIFICATION**
Art. 33 — Notification of a personal data breach.
Triggered when the interaction context involves a potential personal
data breach requiring 72-hour supervisory authority notification.

### Other EU

**EU_CYBER_RESILIENCE_ACT**
Cyber Resilience Act — product security requirements.
Triggered when the interaction involves software or hardware products
with digital elements subject to CRA security obligations.

**EU_PSD2_ART98_STRONG_AUTH**
PSD2 Art. 98 — Strong customer authentication.
Triggered when an authentication event deviates from expected baseline
in a payment services context.

**EU_EIDAS2_TRUST_SERVICE**
eIDAS 2.0 — Trust service requirements.
Triggered when the interaction involves qualified trust services
or electronic identification under eIDAS 2.0.

---

## Germany / BSI (3 flags)

**DE_BSI_GRUNDSCHUTZ_AI_AUDIT**
BSI IT-Grundschutz — AI system audit requirement.
Triggered when the interaction context falls within BSI IT-Grundschutz
baseline protection requirements for AI systems.

**DE_BSI_KRITIS_INCIDENT**
BSI KRITIS — Critical infrastructure incident.
Triggered when the event involves a KRITIS-designated operator and
meets or approaches the threshold for BSI incident reporting.

**DE_BSI_C5_CLOUD_AUDIT**
BSI C5 — Cloud computing compliance audit.
Triggered when the AI system operates on cloud infrastructure subject
to BSI C5 attestation requirements.

---

## United Kingdom (5 flags)

**UK_FCA_PS21_3_OPERATIONAL_RESILIENCE**
FCA PS21/3 — Operational resilience.
Triggered when the event affects an important business service
of an FCA-regulated firm and may breach impact tolerances.

**UK_PRA_SS1_21_OUTSOURCING**
PRA SS1/21 — Outsourcing and third-party risk management.
Triggered when the AI system is a material outsourcing arrangement
and the output indicates a risk management failure.

**UK_FCA_CONSUMER_DUTY**
FCA Consumer Duty — Consumer outcomes.
Triggered when an AI output may result in foreseeable harm to
retail customers or fails the consumer understanding outcome.

**UK_ICO_AI_AUDITING**
ICO — AI auditing framework.
Triggered when the interaction involves automated decision-making
subject to ICO AI auditing guidance.

**UK_NCSC_CAF**
NCSC Cyber Assessment Framework.
Triggered when the event involves UK CNI operators and indicates
a potential CAF objective failure.

---

## United States (9 flags)

**US_NIST_AI_RMF_GOVERN**
NIST AI RMF — Govern function.
Triggered when the AI system lacks documented governance structures
for risk management as required by the NIST AI RMF.

**US_NIST_AI_RMF_MEASURE**
NIST AI RMF — Measure function.
Triggered when the AI output indicates measurement or evaluation
failures in the AI risk management programme.

**US_NIST_AI_RMF_MAP**
NIST AI RMF — Map function.
Triggered when the interaction context reveals gaps in AI risk
identification and categorisation.

**US_SEC_8K_ITEM105_CYBER**
SEC Form 8-K Item 1.05 — Material cybersecurity incidents.
Triggered when the interaction involves a potential material
cybersecurity incident requiring 8-K disclosure within 4 business days.

**US_SEC_REGULATION_SP_SAFEGUARDS**
SEC Regulation S-P — Safeguards Rule.
Triggered when customer financial information may have been exposed
in a manner requiring notification under Reg S-P.

**US_FFIEC_AI_GUIDANCE**
FFIEC — AI in financial services guidance.
Triggered when the AI system is used in financial services
and the output indicates model risk management failures.

**US_HIPAA_SECURITY_RULE**
HIPAA Security Rule — Electronic protected health information.
Triggered when the interaction involves ePHI and the output
indicates a potential security rule violation.

**US_CISA_AI_FRAMEWORK**
CISA — AI cybersecurity framework.
Triggered when the event involves critical infrastructure operators
and the AI output indicates a cybersecurity risk.

**US_EXECUTIVE_ORDER_14110**
Executive Order 14110 — Safe, Secure, and Trustworthy AI.
Triggered when the AI system meets dual-use foundation model
thresholds or involves national security applications.

---

## Australia (5 flags)

**AU_APRA_CPS230_OPERATIONAL_RISK**
APRA CPS 230 — Operational risk management.
Triggered when the AI system is a material service provider
and the output indicates an operational risk event.

**AU_APRA_CPG234_IT_SECURITY**
APRA CPG 234 — Information security.
Triggered when the event indicates an information security
incident for an APRA-regulated entity.

**AU_OAIC_AI_PRIVACY**
OAIC — AI privacy guidance.
Triggered when the AI interaction involves personal information
in a manner inconsistent with Privacy Act 1988 obligations.

**AU_ASIC_RG273_AI_ADVICE**
ASIC RG 273 — Artificial intelligence in financial advice.
Triggered when an AI system provides financial advice without
appropriate disclosure, oversight, or human review.

**AU_ASD_ESSENTIAL_EIGHT**
ASD Essential Eight — Cybersecurity baseline.
Triggered when the event indicates a failure of one or more
ASD Essential Eight mitigation strategies.

---

## Canada (5 flags)

**CA_AIDA_HIGH_IMPACT**
AIDA — High-impact AI system.
Triggered when the AI system meets the AIDA definition of a
high-impact system and the output indicates a harm risk.

**CA_AIDA_HARM_MITIGATION_RECORD**
AIDA — Harm mitigation documentation record.
Indicates this UMI trace is being retained as AIDA harm mitigation
documentation. The trace documents detection and blocking of
a potentially harmful output.

**CA_PIPEDA_AUTOMATED_DECISION**
PIPEDA — Automated decision-making.
Triggered when the AI system makes automated decisions about
individuals using personal information under PIPEDA.

**CA_OSFI_B10_OUTSOURCING**
OSFI B-10 — Outsourcing of business activities.
Triggered when the AI system is a material outsourced function
for an OSFI-regulated institution.

**CA_OSFI_E23_MODEL_RISK**
OSFI E-23 — Model risk management.
Triggered when the AI output indicates model risk management
failures for an OSFI-regulated institution.

---

## Version history

| Version | Flags | Change |
|---------|-------|--------|
| 1.0.0   | 32    | Initial release |
| 1.1.0   | 44    | Added AU, CA jurisdictions |
| 1.1.2   | 47    | Added EU_CYBER_RESILIENCE_ACT, EU_EIDAS2_TRUST_SERVICE, DE_BSI_C5_CLOUD_AUDIT |


---

| Property | Details |
| :--- | :--- |
| **Document version** | 1.1.2 |
| **Date** | March 2026 |
| **Standard** | Universal Morphological Interface (UMI) v1.1.2 |

---

www.umi-standard.org — UMI Standard Regulatory Reference — The UMI Initiative

Copyright 2026 The UMI Initiative
Originally authored by Lukas Pruski
Stewardship provided by Aliventi sp. z o.o.

The UMI standard is licensed under Apache 2.0.
The encoding engine is proprietary and not covered by this licence.
