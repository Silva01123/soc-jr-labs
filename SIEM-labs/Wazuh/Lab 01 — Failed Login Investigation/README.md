# Lab 01 — Failed Login Investigation

## 1. Objective

Investigate failed authentication attempts and understand how a SOC Analyst uses Wazuh to identify suspicious login activity.

## 2. Scenario

A monitored Windows endpoint generates multiple failed login events. The analyst must investigate the events, identify relevant evidence, and determine whether the activity requires further investigation.

**Evidence status:** This lab initially uses simulated data for educational purposes. No real Wazuh alert is claimed unless it is collected from an actual Wazuh environment.

## 3. Tools and Technologies

- Wazuh SIEM
- Windows Security Event Logs
- Windows Event ID 4625 — Failed logon
- Windows Event ID 4624 — Successful logon
- JSON event data and alert fields

## 4. Investigation Objectives

- Identify the account involved.
- Determine the affected endpoint.
- Establish when the failed logins occurred.
- Identify the logon type and failure reason when available.
- Check whether a successful login followed the failures.
- Assess whether the activity is suspicious.
- Document findings and recommend appropriate actions.

## 5. Wazuh Investigation Workflow

1. Locate the relevant authentication alert in Wazuh.
2. Review the alert timestamp, rule description, and severity.
3. Inspect the original event fields.
4. Identify the username, endpoint, source information, and logon type when available.
5. Correlate related failed and successful authentication events.
6. Determine whether additional evidence is required.
7. Classify the activity and document the investigation.

## 6. Evidence

Evidence collected:

- Alert ID:
- Timestamp:
- Wazuh rule ID and description:
- Rule level:
- Agent name:
- Windows Event ID:
- Username:
- Source IP, if available:
- Logon type, if available:
- Related successful login:
- Evidence source: Simulated / Real Wazuh environment

Do not fill in fields with invented values. Record unavailable fields as "Not available".

## 7. Findings

### What happened?

[Describe the authentication activity observed.]

### What evidence supports the conclusion?

[List the relevant event fields and correlated events.]

### Is the activity suspicious?

[Explain the reasoning and any limitations.]

## 8. Classification

- Result: Pending investigation
- Severity: To be determined from the available evidence
- Confidence: To be determined

## 9. Recommended Actions

[Document proportionate next steps based on the evidence, such as reviewing related events, validating the activity with the system owner, or escalating a suspected brute-force attempt.]

## 10. Conclusion

[Summarize what was identified, what remains uncertain, and the next recommended action.]

## 11. Skills Practiced

- Authentication event analysis
- Windows Event ID interpretation
- Wazuh alert investigation
- Event correlation
- Evidence-based incident classification
- SOC investigation documentation
