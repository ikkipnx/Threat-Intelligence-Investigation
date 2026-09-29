# Detection Coverage

## Purpose

This document maps the behaviors identified during the FIN7
investigation to the corresponding detection hypotheses and Sigma rules.

The objective is to demonstrate how threat intelligence findings
can be translated into defensive detection opportunities.

---

## Coverage Matrix

| MITRE ATT&CK | Technique | Observed Behavior | Detection Rule | Telemetry |
|---|---|---|---|---|
| T1204.002 | User Execution: Malicious File | Victim interaction with hidden LNK | suspicious-lnk-execution.yml | Process Creation / File Activity |
| T1218.005 | System Binary Proxy Execution: Mshta | mshta.exe used to execute VBScript | suspicious-mshta.yml | Process Creation |
| T1059.001 | Command and Scripting Interpreter: PowerShell | PowerShell used during payload execution | suspicious-powershell.yml | Process Creation / PowerShell Logs |
| T1053.005 | Scheduled Task/Job: Scheduled Task | Scheduled tasks used for persistence | suspicious-scheduled-task.yml | Process Creation / Task Scheduler |

---

## Detection Coverage by Attack Stage

### User Execution

**Technique:** T1204.002

**Behavior:**
The victim interacted with a malicious attachment, resulting in
execution of a hidden LNK file.

**Detection:**
`suspicious-lnk-execution.yml`

**Required telemetry:**
- Process creation
- File activity
- File path
- Parent process
- User
- Host

---

### Execution - Mshta

**Technique:** T1218.005

**Behavior:**
The hidden LNK initiated `mshta.exe` to execute malicious code.

**Detection:**
`suspicious-mshta.yml`

**Required telemetry:**
- Process creation
- Parent process
- Command line
- User
- Host
- Timestamp

---

### Execution - PowerShell

**Technique:** T1059.001

**Behavior:**
PowerShell was used during the infection chain to execute commands
and retrieve an additional payload.

**Detection:**
`suspicious-powershell.yml`

**Required telemetry:**
- Process creation
- PowerShell command line
- Parent process
- User
- Host
- Network connections

---

### Persistence

**Technique:** T1053.005

**Behavior:**
Scheduled tasks were used as a persistence mechanism.

**Detection:**
`suspicious-scheduled-task.yml`

**Required telemetry:**
- Scheduled task creation
- Task name
- Creating process
- User
- Command
- Host
- Timestamp

---

## Detection Limitations

The current Sigma rules represent basic detection hypotheses.

They identify relevant process activity but do not independently
determine whether an observed event is malicious.

Additional contextual analysis may be required, including:

- Parent-child process relationships
- Command-line analysis
- User and host baselines
- File reputation
- Network activity
- Temporal correlation between events
- Endpoint and SIEM telemetry

The rules have been syntactically validated using Sigma CLI but
were not tested against production telemetry.

---

## Purple Team Opportunity

The detection coverage can be further validated in a controlled
laboratory environment by reproducing representative behaviors
and verifying whether the expected telemetry and detections are
generated.

This would allow comparison between:

- Adversary behavior
- Endpoint telemetry
- Detection logic
- Alert generation
- Analyst investigation

Such validation would extend the project from threat intelligence
and detection engineering toward a Purple Team workflow.
