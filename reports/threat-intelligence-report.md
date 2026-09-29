# Threat Intelligence Report

## FIN7 - Phishing and Malware Infection Chain

---

## 1. Executive Summary

This investigation analyzes documented FIN7 activity involving
spearphishing attachments and a multi-stage malware infection chain.

The investigated activity includes malicious DOCX and RTF files,
user execution, hidden LNK files, mshta.exe, VBScript, PowerShell,
Cobalt Strike infrastructure and the HALFBAKED backdoor.

The investigation identified seven indicators of compromise,
including file hashes, file names, a domain and an IP address.

The observed behaviors were mapped to six MITRE ATT&CK techniques
covering Initial Access, Execution and Persistence.

The analysis is based on publicly available threat intelligence
sources, primarily MITRE ATT&CK and Mandiant.

---

## 2. Threat Actor

Threat Actor: FIN7

MITRE ATT&CK ID: G0046

Associated aliases documented by MITRE include:

- GOLD NIAGARA
- ITG14
- Carbon Spider
- ELBRUS
- Sangria Tempest

FIN7 is associated with financially motivated cyber operations.

This report focuses specifically on the documented infection chain
analyzed during this investigation.

---

## 3. Investigation Objective

The objective of this investigation was to:

- Identify relevant indicators of compromise.
- Enrich the identified indicators with contextual information.
- Reconstruct the documented infection chain.
- Map observed behaviors to MITRE ATT&CK.
- Correlate indicators with artifacts and attack stages.
- Produce structured defensive threat intelligence.

---

## 4. Attack Chain

The investigated infection chain can be summarized as:

Spearphishing Attachment
        ↓
Malicious DOCX / RTF
        ↓
User Execution
        ↓
Hidden LNK
        ↓
mshta.exe
        ↓
VBScript
        ↓
PowerShell
        ↓
Cobalt Strike Stager
        ↓
Command and Control
        ↓
HALFBAKED

This reconstruction is based on the behaviors and relationships
documented by the sources used in this investigation.

---

## 5. Initial Access

FIN7 used spearphishing emails containing malicious Microsoft
Documents or RTF files.

MITRE ATT&CK:

- T1566.001 - Phishing: Spearphishing Attachment

Identified phishing artifacts include:

- Doc33.docx
- Mail.rtf

---

## 6. User Execution

The phishing attachments were designed to induce victim interaction,
resulting in execution of a hidden LNK file.

MITRE ATT&CK:

- T1204.002 - User Execution: Malicious File

---

## 7. Execution

The hidden LNK initiated mshta.exe, which was used to execute
malicious VBScript.

MITRE ATT&CK:

- T1218.005 - System Binary Proxy Execution: Mshta
- T1059.005 - Command and Scripting Interpreter: Visual Basic

The infection chain also included PowerShell.

MITRE ATT&CK:

- T1059.001 - Command and Scripting Interpreter: PowerShell

The identified PowerShell artifact was:

- 58d2a83f777942.26535794.ps1

---

## 8. Persistence

The investigated activity included scheduled tasks as a persistence
mechanism.

MITRE ATT&CK:

- T1053.005 - Scheduled Task/Job: Scheduled Task

---

## 9. Command and Control

The investigation identified infrastructure associated with the
documented infection chain.

### Domain

aaa[.]stage[.]14919005[.]www1[.]proslr3[.]com

Context:

DNS C2 server associated with the Cobalt Strike stager.

### IP Address

198[.]100[.]119[.]6

Context:

C2 server associated with the HALFBAKED backdoor.

---

## 10. Malware

The documented infection chain included the HALFBAKED backdoor.

The investigation also identified artifacts associated with the
execution chain, including VBScript and PowerShell files.

---

## 11. Indicators of Compromise

| Type | Indicator | Context |
|------|-----------|---------|
| MD5 | 6a5a42ed234910121dbb7d1994ab5a5e | Doc33.docx phishing lure |
| MD5 | 1a9e113b2f3caa7a141a94c8bc187ea7 | Mail.rtf phishing lure |
| Domain | aaa[.]stage[.]14919005[.]www1[.]proslr3[.]com | Cobalt Strike stager C2 |
| IP | 198[.]100[.]119[.]6 | HALFBAKED C2 |
| File | 58d2a83f7778d5.36783181.vbs | VBScript launcher |
| File | 58d2a83f777942.26535794.ps1 | PowerShell script |
| File | 58d2a83f777908.23270411.vbs | Second VBScript |

All indicators were collected from the sources documented in this
investigation.

---

## 12. MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique |
|--------|--------------|-----------|
| Initial Access | T1566.001 | Phishing: Spearphishing Attachment |
| Execution | T1204.002 | User Execution: Malicious File |
| Execution | T1218.005 | System Binary Proxy Execution: Mshta |
| Execution | T1059.005 | Command and Scripting Interpreter: Visual Basic |
| Execution | T1059.001 | Command and Scripting Interpreter: PowerShell |
| Persistence | T1053.005 | Scheduled Task/Job: Scheduled Task |

---

## 13. Defensive Considerations

Based on the behaviors identified in this investigation,
organizations can consider monitoring for:

- Suspicious execution of mshta.exe.
- Unexpected VBScript execution.
- PowerShell execution associated with suspicious parent processes.
- LNK files originating from email attachments or user-writable
  directories.
- Scheduled task creation by unusual processes or users.
- Connections to known or suspicious C2 infrastructure.
- Execution chains involving Office documents, LNK files,
  mshta.exe and scripting interpreters.

These considerations should be adapted to the organization's
environment and detection capabilities.

---

## 14. Intelligence Gaps

The investigation does not establish:

- The complete infrastructure associated with the activity.
- All malware samples related to the campaign.
- The complete set of indicators.
- The complete set of MITRE ATT&CK techniques used across the
  broader FIN7 ecosystem.
- Whether the identified infrastructure remains operational.

Additional investigation and independent validation would be
required to establish these relationships.

---

## 15. Confidence Assessment

Overall assessment confidence: High for the specific behaviors and
indicators directly supported by the cited sources.

Confidence is lower for relationships that extend beyond the
specific evidence documented in the investigated campaign.

---

## 16. Sources

### MITRE ATT&CK

FIN7 - G0046

https://attack.mitre.org/groups/G0046/

### Mandiant / Google Cloud

FIN7 Power Hour: Adversary Archaeology and the Evolution of FIN7

https://cloud.google.com/blog/topics/threat-intelligence/evolution-of-fin7/

### Mandiant / Google Cloud

FIN7 Evolution and the Phishing LNK

https://cloud.google.com/blog/topics/threat-intelligence/fin7-phishing-lnk/
