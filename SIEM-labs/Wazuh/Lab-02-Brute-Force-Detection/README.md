# Lab 02 — Brute Force Detection

## 1. Overview

This lab simulates a Security Operations Center (SOC) investigation
involving repeated failed authentication attempts, a subsequent
successful login, and suspicious process creation on a Windows host.

The objective is to identify suspicious authentication patterns,
correlate Windows security events, assess potential account compromise,
and recommend appropriate incident response actions.

**Environment:** Simulated Windows security events  
**SIEM Focus:** Wazuh  
**Investigation Type:** Simulated case study  
**Difficulty:** Beginner  
**Status:** Completed as a simulated investigation exercise

> Important: The events and timestamps in this lab are fictional.
> No live Wazuh alerts were generated or investigated.
> This exercise demonstrates analytical reasoning, not a verified
> detection in a live environment.

---

## 2. Investigation Objectives

- Identify suspicious authentication patterns.
- Understand Windows Event IDs 4625, 4624, and 4688.
- Correlate authentication events with subsequent process creation.
- Assess the possibility of account compromise.
- Identify additional evidence required to support a conclusion.
- Recommend investigation, containment, and escalation actions.
- Document findings in a structured SOC investigation report.

---

## 3. Scenario

A Windows server generates several failed authentication events
followed by a successful login to the administrator account.

Shortly afterward, a PowerShell process is created.

The account owner reports that they were not accessing the server
at the time and do not recognize the activity.

The SOC analyst must determine whether the activity is legitimate,
suspicious, or indicative of a potential security incident.

### Simulated Environment

| Field | Value |
|---|---|
| Host | WIN-SRV-01 |
| Account | administrator |
| Source IP | Unknown |
| Operating System | Windows |
| SIEM | Wazuh (investigation context) |
| Evidence Source | Fictional training scenario |

---

## 4. Evidence Collected

The following events are part of the simulated scenario.

| Time | Event ID | Description |
|---|---|---|
| 14:32:01 | 4625 | Failed login |
| 14:32:03 | 4625 | Failed login |
| 14:32:05 | 4625 | Failed login |
| 14:32:07 | 4625 | Failed login |
| 14:32:09 | 4625 | Failed login |
| 14:32:11 | 4625 | Failed login |
| 14:32:18 | 4624 | Successful login |
| 14:32:25 | 4688 | Process creation |

### Process Information

| Field | Value |
|---|---|
| Process | powershell.exe |
| Parent Process | cmd.exe |
| Full Command Line | Unavailable |
| Execution Context | Requires investigation |

**Evidence limitation:** The source IP, logon type, Logon ID,
complete command line, and associated network activity are unknown.

These details must be collected before drawing a definitive conclusion.

---

## 5. Event Analysis

### Event ID 4625 — Failed Logon

Event ID 4625 records a failed logon attempt.

Six failures occurred within approximately ten seconds against
the same account.

This pattern may indicate repeated password guessing or another
authentication problem.

Further investigation is required to determine whether the attempts
originated from a single source and whether other accounts were targeted.

### Event ID 4624 — Successful Logon

Event ID 4624 records a successful logon.

The successful login occurred seven seconds after the last recorded
failure.

This sequence increases concern because repeated failures were
followed by successful authentication.

However, the sequence alone does not prove that an attacker
successfully compromised the account.

The analyst should examine the source address, logon type, Logon ID,
authentication details, and authorization context.

### Event ID 4688 — Process Creation

Event ID 4688 records the creation of a process when the relevant
Windows auditing is configured.

The scenario includes a PowerShell process whose parent process
was cmd.exe.

PowerShell is a legitimate administrative tool and is not inherently
malicious.

However, its execution shortly after the suspicious authentication
sequence warrants further investigation.

The full command line and related process activity should be collected
if available.

---

## 6. Event Correlation

The simulated timeline is:

1. Multiple failed authentication attempts.
2. A successful login to the administrator account.
3. PowerShell process creation.
4. The account owner denies performing the activity.

The combination of these observations increases the suspicion level.

The events should be correlated using timestamps, host information,
account details, source addresses, and Logon IDs where available.

A shared timeline alone does not establish that all events belong
to the same session or were caused by the same actor.

---

## 7. Investigation Findings

### Observed Indicators

- Six failed logon attempts within approximately ten seconds.
- A successful logon shortly after the failed attempts.
- PowerShell process creation after the successful logon.
- The account owner denies recognizing the activity.

### Missing Evidence

- Source IP address and originating device.
- Logon type and Logon ID.
- Full PowerShell command line.
- PowerShell operational logs, if available.
- Related process execution and network connections.
- Evidence of persistence, privilege escalation, or lateral movement.
- Confirmation of whether the activity was authorized.

These gaps prevent a definitive conclusion about account compromise.

---

## 8. Classification

**Preliminary Classification:** Suspicious Activity  
**Potential Risk:** Unauthorized account access  
**Confirmed Compromise:** Not established  
**Confidence:** Limited by missing evidence

The combination of repeated failed logons, a subsequent successful
login, process creation, and the account owner's denial warrants
continued investigation.

The available evidence does not establish that the account was
compromised or that a brute-force attack was successful.

---

## 9. Recommended Response Actions

### Immediate Investigation

1. Identify the source IP and originating device.
2. Review the failed and successful authentication records.
3. Compare logon types, Logon IDs, timestamps, and account details.
4. Retrieve the full PowerShell command line and relevant execution logs.
5. Examine related processes and network connections.
6. Search for similar authentication patterns affecting other accounts.

### Containment Considerations

If evidence indicates an active compromise, follow the organization's
incident response procedure.

Depending on the findings and the analyst's authorization, appropriate
actions may include:

- Escalating the case to SOC L2 or the incident response team.
- Restricting the affected account or resetting its credentials.
- Isolating a confirmed affected endpoint when justified and authorized.
- Preserving relevant logs and other evidence.

Containment decisions should consider business impact, the risk of
ongoing compromise, and the organization's established procedures.

### Evidence Preservation

Document timestamps, affected assets, relevant event records,
investigation steps, and all response actions.

Maintain the integrity of collected evidence and follow the
organization's evidence-handling procedures.

---

## 10. Wazuh Investigation Approach

In a live Wazuh environment, an analyst could use available Windows
security telemetry to investigate this scenario.

The investigation would depend on the Windows agent configuration,
enabled audit policies, collected event channels, and available fields.

Potential investigation steps include:

1. Locate relevant authentication events.
2. Filter by host and account.
3. Examine the event timestamps and source information.
4. Investigate process creation records.
5. Correlate the events using available fields.
6. Review related alerts and records for additional indicators.

**Validation status:** These steps describe a proposed Wazuh workflow.
They were not executed against a live Wazuh deployment for this lab.

No actual Wazuh detection rule, alert, or incident was validated.

---

## 11. Lessons Learned

- Repeated failed logons can indicate suspicious authentication activity.
- A successful login after repeated failures deserves investigation.
- Event ID 4688 can provide valuable process creation evidence.
- Legitimate tools such as PowerShell may be used for both administration
  and malicious activity.
- Event correlation strengthens an investigation but does not
  automatically prove causation.
- An account owner's denial is relevant context, not conclusive
  technical evidence.
- SOC analysts should distinguish observed facts from hypotheses.
- Containment should be proportionate, authorized, and evidence-based.

---

## 12. Final Conclusion

The simulated scenario contains multiple indicators that justify
further investigation for potential unauthorized account access.

The repeated failed logons, subsequent successful authentication,
PowerShell process creation, and account owner's denial collectively
increase suspicion.

However, the source of the activity, the legitimacy of the session,
and the purpose of the PowerShell execution remain unverified.

The appropriate next step is to collect additional evidence,
continue the investigation, and escalate according to the
organization's incident response procedures.

The case remains classified as suspicious activity rather than
a confirmed compromise.

---

## 13. Lab Status

- Investigation type: Simulated
- Authentication event analysis: Completed
- Event correlation: Completed for the simulated scenario
- Preliminary classification: Suspicious activity
- Response recommendations: Documented
- Live Wazuh alert validation: Not performed
- Confirmed account compromise: Not established
- Final status: Completed as a simulated investigation exercise
