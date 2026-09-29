# Detection Hypotheses

## Purpose

This document translates the behaviors identified during the FIN7
investigation into defensive detection opportunities.

The hypotheses are derived from publicly documented FIN7 activity
and are intended for research and detection engineering purposes.

These are detection hypotheses and were not validated against a
production environment.

---

## 1. Suspicious mshta.exe Execution

### Observed Behavior

FIN7 used `mshta.exe` to execute malicious VBScript.

### MITRE ATT&CK

- T1218.005 - System Binary Proxy Execution: Mshta

### Detection Hypothesis

Monitor process creation events involving `mshta.exe`, particularly
when the process is launched by unusual parent processes or with
suspicious command-line parameters.

### Relevant Telemetry

- Process creation
- Parent process
- Command line
- User
- Host
- Timestamp

### Investigation Questions

- Which process spawned `mshta.exe`?
- Was the execution initiated from an Office application?
- Was a script or remote resource referenced?
- Is the execution associated with a known user or host activity?

---

## 2. Suspicious PowerShell Execution

### Observed Behavior

FIN7 used PowerShell to launch shellcode and retrieve an additional
payload.

### MITRE ATT&CK

- T1059.001 - Command and Scripting Interpreter: PowerShell

### Detection Hypothesis

Monitor PowerShell executions with suspicious command-line
characteristics, unusual parent processes or unexpected network
activity.

### Relevant Telemetry

- Process creation
- PowerShell command line
- Parent process
- User
- Host
- Network connections

### Investigation Questions

- What process launched PowerShell?
- What command or script was executed?
- Was encoded or obfuscated content present?
- Did PowerShell initiate external network communication?

---

## 3. Suspicious LNK Execution

### Observed Behavior

FIN7 used hidden LNK files as part of the infection chain.

### MITRE ATT&CK

- T1204.002 - User Execution: Malicious File

### Detection Hypothesis

Monitor execution of LNK files originating from email attachments,
temporary directories or other user-writable locations.

### Relevant Telemetry

- File creation
- Process creation
- File path
- Parent process
- User
- Host

### Investigation Questions

- Where did the LNK file originate?
- Which process executed the LNK?
- Was `mshta.exe`, PowerShell or another scripting interpreter
  launched afterward?

---

## 4. Suspicious Scheduled Task Creation

### Observed Behavior

FIN7 has used scheduled tasks as a persistence mechanism.

### MITRE ATT&CK

- T1053.005 - Scheduled Task/Job: Scheduled Task

### Detection Hypothesis

Monitor the creation of scheduled tasks by unusual users,
applications or processes.

### Relevant Telemetry

- Scheduled task creation
- Task name
- Creating process
- User
- Command
- Host
- Timestamp

### Investigation Questions

- Which process created the task?
- Which executable or script does the task execute?
- Is the task associated with a legitimate software installation?
- Was the task created shortly after another suspicious event?

---

## Detection Engineering Opportunity

The behaviors identified during the investigation provide several
opportunities to develop and validate detection logic.

Potential detection coverage includes:

- `mshta.exe` execution
- Suspicious PowerShell activity
- LNK-based execution
- Scheduled task creation
- Correlation between scripting activity and suspicious network
  connections

Further validation would require representative telemetry from a
controlled laboratory environment.
