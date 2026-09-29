# Threat Intelligence Investigation — FIN7

## Overview

This project documents a Cyber Threat Intelligence (CTI) investigation
of publicly documented FIN7 activity.

The investigation focuses on the reconstruction of a malware infection
chain, identification and enrichment of Indicators of Compromise (IOCs),
mapping of observed behaviors to MITRE ATT&CK, and production of a
structured threat intelligence report.

> This is a research and laboratory project based on publicly available
> threat intelligence sources. It does not represent an operational
> investigation conducted against a real organization.

---

## Investigation Objective

The objective of this investigation is to:

- Identify relevant Indicators of Compromise (IOCs).
- Enrich indicators with contextual information.
- Analyze the documented infection chain.
- Identify adversary behaviors and TTPs.
- Map observed behaviors to MITRE ATT&CK.
- Correlate indicators with artifacts and attack stages.
- Produce defensive threat intelligence.

---

## Threat Actor

**FIN7**

**MITRE ATT&CK ID:** G0046

Associated aliases documented by MITRE include:

- GOLD NIAGARA
- ITG14
- Carbon Spider
- ELBRUS
- Sangria Tempest

---

## Investigation Workflow

```text
OSINT
  ↓
IOC Collection
  ↓
IOC Enrichment
  ↓
TTP Analysis
  ↓
MITRE ATT&CK Mapping
  ↓
IOC / TTP Correlation
  ↓
Attack Chain Reconstruction
  ↓
Threat Intelligence Report
