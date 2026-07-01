# Windows Persistence Investigation Lab

## Objective

The purpose of this lab was to investigate common Windows persistence mechanisms that allow applications or malicious software to automatically execute after system startup or user logon.

The investigation focused on identifying legitimate startup locations commonly reviewed during security monitoring and incident response activities.

---

## Tools Used

- Registry Editor (regedit)
- Windows Run Dialog
- File Explorer

---

## Investigation

Several Windows locations commonly associated with persistence were investigated.

### 1. User Startup Folder

The following location was accessed using the Run dialog:

```text
shell:startup
```

This folder contains applications configured to start automatically for the currently logged-in user.

The Startup folder was inspected and found to be empty.

---

### 2. Common Startup Folder

The following location was accessed:

```text
shell:common startup
```

This folder contains applications configured to start automatically for all users of the system.

The Common Startup folder was inspected and found to be empty.

---

### 3. User AppData Directory

The following directory was reviewed:

```text
%AppData%
```

The AppData folder was inspected for unusual directories or suspicious application names.

Only expected application folders associated with legitimate installed software were observed.

No suspicious files or directories were identified.

---

### 4. Temporary Files Directory

The following directory was reviewed:

```text
%TEMP%
```

Temporary files and folders were inspected for unusual executable files or suspicious naming patterns.

The contents appeared consistent with normal Windows and application activity.

No suspicious executable files or persistence mechanisms were identified.

---

### 5. Registry Run Keys

Previously identified registry startup locations were reviewed as part of the persistence investigation.

User-level startup entries:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Observed entries:

- Microsoft Edge
- OneDrive
- Steam

System-level startup entries:

```text
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
```

Observed entries:

- RTKAUDUSERVICE
- SecurityHealth

All registry entries were reviewed and determined to belong to legitimate Windows components or installed applications.

---

## Security Relevance

Persistence is a common technique used by attackers to maintain access to a compromised system after reboot or user logon.

SOC analysts frequently inspect locations such as:

- Registry Run Keys
- Startup Folders
- AppData directories
- Temporary file locations

These areas are commonly abused by malware to automatically execute malicious code.

Understanding these persistence mechanisms is essential during endpoint investigations and incident response activities.

---

## Results

- Investigated user and system startup folders.
- Reviewed AppData and Temporary directories.
- Verified registry startup entries.
- Identified only legitimate startup applications.
- No suspicious persistence mechanisms were detected.

---

## Conclusion

A Windows persistence investigation was successfully performed by examining several common persistence locations used by both legitimate software and potential malware.

The investigation included Startup folders, registry Run keys, AppData, and Temporary directories.

All observed entries were consistent with normal system operation, and no indicators of malicious persistence were identified.

This lab provided practical experience with Windows persistence mechanisms and demonstrated how SOC analysts validate startup locations during endpoint investigations.
