# Windows Security Investigation Lab

## Objective

The purpose of this lab was to investigate the security posture of a Windows endpoint by reviewing its built-in security features.

The investigation focused on validating the operational status of Microsoft Defender, Windows Firewall, and Windows Update to ensure the system was properly protected.

---

## Tools Used

- Windows Security
- Microsoft Defender
- Windows Firewall
- Windows Update

---

## Investigation

The Windows Security application was used to review the system's security configuration.

### 1. Microsoft Defender

The Virus & threat protection section was reviewed.

Status observed:

```text
No actions needed
```

The investigation confirmed that Microsoft Defender was active and no security alerts or recommended actions were present.

---

### 2. Windows Firewall

The Firewall & network protection section was reviewed.

Observed configuration:

- Active Profile: Public Network
- Windows Firewall: Enabled

The active firewall profile was verified and confirmed to be protecting the endpoint.

---

### 3. Windows Update

The Windows Update section was reviewed.

The system reported:

```text
System is up to date.
```

No pending updates were identified during the investigation.

---

## Security Relevance

Windows built-in security features provide the first layer of defense against malware and unauthorized network activity.

SOC analysts frequently verify:

- Antivirus operational status
- Firewall configuration
- System patch level

These checks help determine whether endpoint protection mechanisms are functioning correctly and whether additional investigation is required.

---

## Results

- Microsoft Defender was operational.
- No security alerts were identified.
- Windows Firewall was enabled.
- The active network profile was successfully verified.
- Windows Update confirmed the system was fully updated.
- No security misconfigurations were detected.

---

## Conclusion

A Windows security investigation was successfully performed using the built-in Windows Security application.

The investigation confirmed that Microsoft Defender, Windows Firewall, and Windows Update were operating as expected.

The endpoint demonstrated a healthy security posture, and no indicators of disabled protection or security misconfiguration were identified.
