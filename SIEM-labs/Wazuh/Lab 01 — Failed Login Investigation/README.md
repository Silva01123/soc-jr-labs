# Lab 01 — Failed Login Investigation

## 1. Objective

Investigate failed authentication attempts and learn how a SOC Analyst uses Wazuh concepts and Windows Security events to identify and assess suspicious login activity.

## 2. Scenario

A Windows endpoint records multiple failed authentication attempts, followed by a successful login and subsequent process creation. The analyst must correlate events, identify relevant evidence, assess potential risks, and recommend appropriate actions.

**Evidence Status:** Simulated training scenario. No real Wazuh alerts were collected.

## 3. Tools and Technologies

- Wazuh SIEM
- Windows Security Event Logs
- Event ID 4625 — Failed logon
- Event ID 4624 — Successful logon
- Event ID 4688 — Process creation
- JSON event data and alert fields
- Authentication and process event correlation

## 4. Investigation Objectives

- Identify the account involved.
- Determine the affected endpoint and source IP.
- Establish the timeline of authentication events.
- Identify suspicious authentication patterns.
- Investigate process creation following successful authentication.
- Determine what additional evidence is required.
- Classify the activity based on available evidence.
- Document findings and recommend appropriate actions.

## 5. Investigation Workflow

1. Locate relevant authentication alerts in Wazuh.
2. Review timestamps, rule descriptions, and severity levels.
3. Inspect the underlying Windows Security events.
4. Identify the username, endpoint, source information, and logon type when available.
5. Correlate failed authentication attempts with subsequent successful logins.
6. Investigate related process creation and available command-line details.
7. Assess the activity using supporting evidence.
8. Classify the activity and determine whether escalation is necessary.
9. Document findings, limitations, and recommended actions.

**Note:** This exercise uses simulated events to practice the investigation methodology. No live Wazuh alerts, rule IDs, or agent data are claimed.

## 6. Evidence

**Evidence Source:** Simulated training data.

### Authentication Events

- Affected endpoint: `WIN-SRV-01`
- Username: `administrator`
- Source IP: `192.168.1.50`
- Failed authentication attempts: 5
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

- Alert ID: Not available
- Wazuh rule ID and description: Not available
- Wazuh rule level: Not available
- Wazuh agent ID: Not available
- Logon type: Not available
- Logon ID: Not available

**Evidence limitation:** These values belong to a simulated scenario and were not extracted from a live Wazuh dashboard or Windows endpoint. Missing fields have not been inferred.

## 7. Findings

### What happened?

Five failed authentication attempts occurred for the `administrator` account within approximately 12 seconds. A successful login occurred 18 seconds after the last recorded failure.

A subsequent process creation event recorded `powershell.exe`, launched by `cmd.exe`.

### What evidence supports the assessment?

The simulated sequence contains:

- Repeated failed authentication attempts.
- A subsequent successful authentication for the same account and source.
- Process creation following the successful login.
- A common simulated endpoint, username, and source IP across the authentication events.

### Is the activity suspicious?

Yes. The sequence warrants further investigation because repeated authentication failures followed by a successful login may indicate a brute-force attempt or another unauthorized authentication scenario.

The subsequent creation of PowerShell through Command Prompt also requires investigation.

However, the available events do not independently prove malicious activity. Legitimate administrative tasks and other benign explanations must also be considered.

## 8. Classification

- **Result:** Suspicious activity — further investigation required
- **Severity:** Undetermined
- **Confidence:** Preliminary
- **Incident confirmed:** No
- **Escalation:** Recommend escalation to SOC Level 2 if the activity remains unexplained or meets the organization's escalation criteria.

## 9. Recommended Actions

1. Identify the device associated with source IP `192.168.1.50`.
2. Confirm whether the administrator login was authorized.
3. Review the complete authentication events and available logon details.
4. Correlate authentication events using timestamps and available session identifiers, such as Logon ID.
5. Investigate the full PowerShell command line and related process activity.
6. Review available PowerShell logs, additional process events, and relevant network activity.
7. Search for other suspicious authentication attempts and privilege-related events.
8. Preserve relevant evidence and document the investigation timeline.
9. Escalate according to the organization's incident response procedures when justified by the evidence.

Any containment action should follow organizational procedures and the assessed risk.

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
- Evidence documentation
- Preliminary incident classification
- SOC escalation decisions
- Wazuh investigation methodology

## 12. Lessons Learned

- Repeated authentication failures must be assessed in context.
- A successful login following multiple failures increases the need for investigation but does not prove compromise.
- Process creation events provide context about activity after authentication.
- Missing evidence must be identified rather than invented.
- Incident classification and escalation decisions must be evidence-based.
- Simulated exercises demonstrate analytical reasoning but do not replace hands-on experience with a live SIEM.

## 13. Lab Status

- **Investigation type:** Simulated
- **Scenario analysis:** Completed
- **Event correlation:** Completed for the simulated scenario
- **Preliminary classification:** Suspicious activity
- **Live Wazuh alert validation:** Not performed
- **Final status:** Completed as a simulated investigation exercise

This lab demonstrates an evidence-based investigation methodology using simulated Windows Security events. It does not claim that a real Wazuh alert was generated or investigated.
