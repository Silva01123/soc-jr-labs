# Windows Registry Investigation Lab

## Objective

The purpose of this lab was to investigate the Windows Registry structure, understand the difference between user-specific and system-wide registry hives, and identify registry locations commonly used for automatic program execution and persistence.

This investigation focused on registry keys frequently reviewed during security monitoring and incident response activities.

---

## Tools Used

- Registry Editor (regedit)
- Windows Operating System

---

## Registry Areas Investigated

### HKEY_CURRENT_USER (HKCU)

The HKCU hive stores configuration settings and preferences for the currently logged-in user.

Path investigated:

```text
HKEY_CURRENT_USER\Software
```

This location contains application-specific settings and user-related configurations.

---

### HKEY_LOCAL_MACHINE (HKLM)

The HKLM hive stores system-wide configuration settings that apply to all users on the computer.

Path investigated:

```text
HKEY_LOCAL_MACHINE\Software
```

This location contains operating system settings, installed software information, and machine-level configurations.

---

## Investigation

The Registry Editor was opened and the following locations were reviewed:

### User Startup Entries

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
```

This registry key is used to automatically launch applications when the current user logs in.

The following entries were identified:

- Microsoft Edge
- OneDrive
- Steam

These entries were reviewed and determined to be legitimate applications configured to start automatically during user logon.

---

### System Startup Entries

```text
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
```

This registry key is used to automatically launch applications for all users of the system.

The following entries were identified:

- RTKAUDUSERVICE
- SecurityHealth

These entries were reviewed and determined to be legitimate components associated with the Realtek audio driver and Windows Security.

---

## Security Relevance

Registry Run keys are commonly reviewed during security investigations because they can be abused by attackers to establish persistence.

Malicious software may create registry entries within:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

or

```text
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

to automatically execute after a system reboot or user logon.

For this reason, these locations are frequently inspected by SOC analysts and incident responders when investigating suspicious activity.

---

## Results

- Successfully navigated the Windows Registry structure.
- Identified the purpose of HKCU and HKLM registry hives.
- Investigated user-level and system-level startup registry keys.
- Reviewed automatic startup entries configured on the system.
- Verified that all identified entries were legitimate and expected.
- No suspicious or unauthorized registry entries were detected.

---

## Conclusion

A Windows Registry investigation was successfully performed using Registry Editor.

The lab provided practical experience navigating registry hives, understanding the distinction between user-specific and system-wide configurations, and identifying registry locations commonly associated with automatic execution and persistence mechanisms.

The investigation confirmed that all startup entries observed during the analysis were legitimate and consistent with normal system operation.

No indicators of malicious persistence were identified.
