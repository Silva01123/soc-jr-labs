# Lab 01 — Failed Login Investigation

## 1. Objective

Investigate failed authentication attempts and learn how a SOC Analyst uses Wazuh concepts and Windows Security events to identify and assess suspicious login activity.

## 2. Scenario

A monitored Windows endpoint records multiple failed authentication attempts, followed by a successful login and subsequent process creation. The analyst must correlate the events, identify relevant evidence, assess potential risks, and recommend appropriate actions.

**Evidence Status:** Simulated training scenario. No real Wazuh alerts were collected, and no live Wazuh investigation is claimed.

## 3. Tools and Technologies

- Wazuh SIEM concepts
- Windows Security Event Logs
- Windows Event ID 4625 — Failed logon
- Windows Event ID 4624 — Successful logon
- Windows Event ID 4688 — Process creation
- JSON event data and alert fields
- Authentication and process event correlation

## 4. Investigation Objectives

- Identify the account involved in the authentication events.
- Determine the affected endpoint and source IP.
- Establish the timeline of failed and successful logins.
- Identify suspicious authentication patterns.
- Investigate process creation following successful authentication.
- Determine which additional evidence is required.
- Classify the activity based on available evidence.
- Document findings and recommend appropriate actions.

## 5. Wazuh Investigation Workflow

1. Locate relevant authentication alerts in Wazuh.
2. Review alert timestamps, rule descriptions, and severity levels.
3. Inspect the underlying Windows Security events.
4. Identify the username, endpoint, source information, and logon type when available.
5. Correlate failed authentication attempts with subsequent successful logins.
6. Investigate related process creation and available command-line details.
7. Assess the activity using supporting evidence.
8. Classify the activity and determine whether escalation is necessary.
9. Document findings, limitations, and recommended actions.

**Note:** This lab demonstrates the investigation methodology using simulated events. Actual Wazuh alerts, rule IDs, and agent data must be collected from a real Wazuh environment before they can be documented as real evidence.

## 6. Evidence

**Evidence Source:** Simulated training data.

### Authentication Events

- Affected endpoint: `WIN-SRV-01`
- Username: `administrator`
- Source IP: `192.168.1.50`
- Failed authentication events: 5
- First failed login: `02:14:32`
- Last failed login: `02:14:44`
- Windows Event ID: `4625`
- Successful login: `02:15:02`
- Windows Event ID: `4624`

### Process Creation Event

- Timestamp: `02:15:15`
- Username: `administrator`
- Process created: `powershell.exe`
- Parent process: `cmd.exe`
- Windows Event ID: `4688`
- Full command line: Not available

### Wazuh Alert Information

- Alert ID: Not available — simulated scenario
- Wazuh rule ID and description: Not available
- Wazuh rule level: Not available
- Wazuh agent ID: Not available
- Logon type: Not available
- Logon ID: Not available

**Evidence limitation:** These values describe a simulated scenario and are not extracted from a live Wazuh dashboard or Windows endpoint. No missing fields have been inferred.

## 7. Findings

### What happened?

Five failed authentication attempts were recorded for the `administrator` account within approximately 12 seconds. A successful login occurred 18 seconds after the last failed attempt.

Shortly afterward, a process creation event recorded `powershell.exe` with `cmd.exe` as its parent process.

### What evidence supports the assessment?

The simulated event sequence contains:

- Repeated failed authentication attempts.
- A subsequent successful authentication for the same account and source.
- Process creation following the successful login.
- A common simulated endpoint, username, and source IP across the authentication events.

### Is the activity suspicious?

Yes. The sequence warrants further investigation because repeated authentication failures followed by a successful login may indicate a potential brute-force attempt or another unauthorized authentication scenario.

The subsequent creation of PowerShell through Command Prompt also requires investigation.

However, neither the authentication sequence nor the process creation event independently proves malicious activity. Legitimate administrative tasks and other benign explanations must also be considered.

## 8. Classification

- **Result:** Suspicious activity — further investigation required
- **Severity:** Undetermined
- **Confidence:** Preliminary
- **Incident confirmed:** No
- **Escalation:** Recommend escalation to SOC Level 2 if the activity remains unexplained or meets the organization's escalation criteria.

## 9. Recommended Actions

1. Identify the device associated with source IP `192.168.1.50`.
2. Confirm whether the administrator login was authorized.
3. Review the complete Windows authentication events and available logon details.
4. Correlate authentication events using timestamps and available session identifiers, such as Logon ID.
5. Investigate the full PowerShell command line and related process activity.
6. Review available PowerShell logs, additional process events, and relevant network activity.
7. Search for other suspicious authentication attempts or privilege-related events.
8. Preserve relevant evidence and document the investigation timeline.
9. Escalate to SOC Level 2 according to the organization's incident response procedures when justified by the evidence.

Any containment action should follow the organization's response procedures and the assessed risk.

## 10. Conclusion

This simulated investigation demonstrates how a SOC Analyst can correlate repeated failed authentication attempts, a subsequent successful login, and process creation to identify potentially suspicious activity.

The appropriate response is to validate the source, investigate the authentication session, examine subsequent process activity, preserve relevant evidence, and escalate when warranted.

The available simulated evidence supports a preliminary suspicious classification but does not confirm an attack or system compromise.

No real Wazuh alerts were investigated during this exercise.

## 11. Skills Practiced

- Windows authentication event analysis
- Event ID interpretation: 4625, 4624, and 4688
- Authentication timeline reconstruction
- Event correlation
- Process investigation
- Evidence collection and documentation
- Preliminary incident classification
- SOC escalation decisions
- Wazuh investigation workflow concepts

## 12. Lessons Learned

- Repeated authentication failures should be assessed in context.
- A successful login following multiple failures increases the need for investigation but does not prove compromise.
- Process creation events provide useful context about activity after authentication.
- Missing evidence must be identified rather than invented.
- Incident classification and escalation decisions must be supported by evidence.
- Simulated exercises demonstrate analytical reasoning but do not replace hands-on experience with a live SIEM.
