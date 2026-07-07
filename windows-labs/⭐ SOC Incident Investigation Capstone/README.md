# ⭐ Final SOC Investigation Scenario (Capstone Project)

## Overview

This capstone project simulates a real-world Security Operations Center (SOC) investigation involving a potential malware infection on a Windows endpoint.

The objective was to investigate a high-severity security alert by collecting evidence, validating suspicious activity, correlating multiple data sources, and determining the appropriate incident response actions.

Unlike the previous labs, this investigation combines all previously acquired Windows security knowledge into a complete endpoint investigation.

---

# Scenario

A Security Information and Event Management (SIEM) platform generated the following alert:

**Alert Name:** Possible Malware Persistence

**Severity:** High

**Endpoint:** PAVILIONHPVS

**User:** Sant'Ana

The alert indicated:

- Suspicious process creation
- Outbound network communication
- Possible persistence mechanism
- Authentication activity requiring investigation

The objective was to determine whether the endpoint had been compromised.

---

# Investigation Methodology

The investigation followed a structured SOC workflow:

1. Alert Validation
2. Process Investigation
3. Process Legitimacy Verification
4. Network Connection Analysis
5. Threat Intelligence Correlation
6. Persistence Investigation
7. Evidence Correlation
8. Incident Assessment
9. Containment Recommendation

---

# Investigation

## 1. Alert Validation

The SIEM detected the execution of a suspicious process:

```
chrome_update.exe
PID: 7648
```

Because the process name imitated legitimate Google Chrome components, additional investigation was required.

---

## 2. Process Verification

The process was investigated to determine its legitimacy.

Collected information:

- Process Name: chrome_update.exe
- Company: Not Available
- Digital Signature: Not Signed

Executable location:

```
C:\Users\Sant'Ana\AppData\Roaming\ChromeUpdate\
```

The executable was not located inside the expected Google Chrome installation directory.

The absence of both a digital signature and company information significantly increased the level of suspicion.

---

## 3. Network Investigation

The process network activity was analyzed.

The investigation identified an active outbound HTTPS connection.

Threat Intelligence analysis reported:

- Remote IP classified as malicious
- Known Command & Control (C2) infrastructure
- Associated with malware hosting and data exfiltration

This evidence strongly suggested malicious behavior.

---

## 4. Persistence Investigation

Windows Registry persistence mechanisms were reviewed.

Registry Path:

```
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

A suspicious autorun entry was identified:

```
ChromeUpdate

C:\Users\Sant'Ana\AppData\Roaming\ChromeUpdate\chrome_update.exe
```

This configuration ensured automatic execution whenever the user logged into Windows.

---

## 5. Evidence Correlation

The collected evidence was correlated to determine the overall security impact.

| Investigation Area | Result |
|--------------------|--------|
| Process Name | Suspicious |
| Executable Location | Unusual (AppData) |
| Digital Signature | Missing |
| Company Information | Missing |
| Network Activity | Active |
| Threat Intelligence | Malicious IP |
| Registry Persistence | Confirmed |

Multiple independent indicators supported the conclusion that the endpoint had likely been compromised.

---

# Timeline

```
08:42:49

Suspicious executable created

↓

08:42:51

Process execution detected

↓

08:43:12

SIEM generated High Severity Alert

↓

Outbound connection established

↓

Threat Intelligence identified malicious C2

↓

Registry persistence confirmed
```

---

# Incident Assessment

Based on the collected evidence, the alert was determined to be a **True Positive**.

Indicators supporting this conclusion included:

- Suspicious process name designed to imitate legitimate software
- Execution from an unusual directory
- Missing digital signature
- Missing publisher information
- Communication with a known malicious Command & Control server
- Registry persistence mechanism configured for automatic execution

The combination of these indicators strongly suggested malware activity.

---

# Response Recommendation

Following standard SOC procedures, the recommended actions were:

- Collect and preserve investigation evidence.
- Isolate the affected endpoint from the network.
- Escalate the incident to the Tier 2 / Incident Response team.
- Perform malware eradication and forensic analysis.
- Remove persistence mechanisms.
- Validate system integrity before returning the endpoint to production.

---

# Skills Demonstrated

- Windows Process Investigation
- Process Validation
- Network Connection Analysis
- Threat Intelligence Correlation
- Windows Registry Analysis
- Persistence Detection
- Security Event Correlation
- Incident Analysis
- Security Documentation
- Incident Response Workflow

---

# Conclusion

This investigation simulated a complete endpoint security incident from initial detection to containment recommendations.

The investigation demonstrated how multiple sources of evidence—including process analysis, network activity, registry persistence, and threat intelligence—can be correlated to accurately determine the nature of a security incident.

The alert was successfully validated as a True Positive, and appropriate containment and escalation actions were identified according to standard SOC incident response practices.
