# Windows Event Log Investigation Lab

## Objective

The purpose of this lab was to investigate Windows Security Event Logs and understand how security-related events are interpreted during endpoint investigations.

The investigation focused on analyzing authentication events, privileged logons, and event correlation to distinguish normal system activity from potentially suspicious behavior.

---

## Tools Used

- Event Viewer
- Windows Security Log

---

## Investigation

The Windows Security log was reviewed using Event Viewer.

The investigation focused on three commonly analyzed Security Event IDs.

### 1. Event ID 4624 – Successful Logon

The latest successful logon event was reviewed.

Observed information:

- Account: SYSTEM
- Logon Type: 5 (Service Logon)

The event indicated that a Windows service successfully authenticated using the built-in SYSTEM account.

This behavior is expected during normal operating system activity.

---

### 2. Event ID 4625 – Failed Logon

Previously identified failed logon events were reviewed.

The investigation confirmed:

- Multiple failed authentication attempts.
- Failed logons associated with the same user account.
- Authentication failure caused by an incorrect username or password.
- Localhost (127.0.0.1) identified as the source.

The activity was analyzed and determined to be consistent with normal local authentication failures.

---

### 3. Event ID 4672 – Special Privileges Assigned

The most recent Event ID 4672 was reviewed.

Observed information:

- Account: SYSTEM
- Domain: NT AUTHORITY

The event included several administrative privileges such as:

- SeDebugPrivilege
- SeBackupPrivilege
- SeRestorePrivilege
- SeLoadDriverPrivilege
- SeTakeOwnershipPrivilege

These privileges were assigned to the Windows SYSTEM account and were determined to be part of normal operating system behavior.

---

## Event Correlation

The investigation demonstrated how multiple Windows Security events can be correlated during an incident investigation.

Observed sequence:

```text
4624
Successful Service Logon (SYSTEM)

↓

4672
Administrative Privileges Assigned (SYSTEM)
```

This sequence represents expected Windows behavior during service initialization.

The previously investigated Event ID 4625 was also considered to understand failed authentication attempts and how authentication events relate to successful logons and privileged sessions.

---

## Security Relevance

Windows Security Event Logs provide valuable information for detecting unauthorized access, privilege escalation, and suspicious authentication activity.

SOC analysts commonly investigate:

- Successful logons
- Failed logons
- Administrative privilege assignments
- Authentication timelines
- Event correlation

Understanding these events is essential during security monitoring and incident response.

---

## Results

- Reviewed successful authentication events.
- Investigated failed authentication attempts.
- Analyzed privileged logon events.
- Correlated multiple Security Event IDs.
- Verified that all observed events were consistent with legitimate Windows system activity.
- No indicators of malicious authentication behavior were identified.

---

## Conclusion

A Windows Security Event Log investigation was successfully performed using Event Viewer.

The investigation provided practical experience analyzing authentication events, privileged logons, and event correlation techniques commonly used by SOC analysts.

All reviewed events were determined to represent expected operating system behavior, and no suspicious authentication activity or privilege abuse was identified.
