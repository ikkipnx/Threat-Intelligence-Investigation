# FIN7 - Attack Chain Analysis

## Overview

The investigated FIN7 activity demonstrates an infection chain
beginning with spearphishing attachments and progressing through
user execution, LNK execution, mshta.exe, VBScript, PowerShell,
Cobalt Strike and C2 infrastructure.

## Attack Chain

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

## Initial Access

FIN7 used spearphishing emails containing malicious Microsoft
Documents or RTF files.

MITRE ATT&CK:
- T1566.001 - Phishing: Spearphishing Attachment

## User Execution

The victim was lured into interacting with the malicious
attachment, resulting in execution of a hidden LNK file.

MITRE ATT&CK:
- T1204.002 - User Execution: Malicious File

## Execution

The hidden LNK initiated mshta.exe, which was used to execute
VBScript.

MITRE ATT&CK:
- T1218.005 - System Binary Proxy Execution: Mshta
- T1059.005 - Command and Scripting Interpreter: Visual Basic

PowerShell was subsequently used in the infection chain to
launch shellcode and retrieve an additional payload.

MITRE ATT&CK:
- T1059.001 - Command and Scripting Interpreter: PowerShell

## Command and Control

The investigation identified C2 infrastructure associated with
the infection chain:

- Domain:
  aaa[.]stage[.]14919005[.]www1[.]proslr3[.]com

- IP:
  198[.]100[.]119[.]6

The domain was associated with the Cobalt Strike stager, while
the IP address was associated with the HALFBAKED C2 server.

## Persistence

The investigated campaign also included scheduled tasks as a
persistence mechanism.

MITRE ATT&CK:
- T1053.005 - Scheduled Task/Job: Scheduled Task

## Malware

The infection chain included the HALFBAKED backdoor.

## Intelligence Assessment

The available evidence supports an infection chain involving:

1. Spearphishing
2. Malicious document
3. User execution
4. Hidden LNK
5. mshta.exe
6. VBScript
7. PowerShell
8. Cobalt Strike
9. Command and Control
10. HALFBAKED

Further investigation would be required to establish additional
relationships between the identified indicators, infrastructure,
malware and threat actor activity.
