# Linux SOC Lab 7 - File System & IOC Hunt

## Objective

The purpose of this lab was to investigate the Linux file system for potential Indicators of Compromise (IOCs), including suspicious files, executable payloads, and privileged binaries.

---

## Commands Used

```bash
ls -la /tmp

find /tmp -type f -executable

sudo find /tmp -type f -executable

find / -perm -4000 -type f 2>/dev/null

ls -l /usr/bin/sudo.ws

file /usr/bin/sudo.ws
```

---

## Investigation Steps

### 1. Temporary Directory Inspection

The `/tmp` directory was inspected because attackers frequently use temporary locations to store malware, scripts, or payloads.

Result:

- No suspicious files found.
- Only legitimate system directories were present.
- No executable files were detected.

---

### 2. Executable File Search

A search was performed for executable files inside `/tmp`.

Result:

- No executable files were identified.

---

### 3. SUID Binary Enumeration

SUID binaries were enumerated to identify files capable of running with elevated privileges.

Command:

```bash
find / -perm -4000 -type f 2>/dev/null
```

Several legitimate system binaries were identified, including:

- passwd
- sudo.ws
- su
- mount
- umount
- chfn
- chsh
- gpasswd
- fusermount3

---

### 4. File Validation

The file `/usr/bin/sudo.ws` was selected for further analysis.

Commands:

```bash
ls -l /usr/bin/sudo.ws

file /usr/bin/sudo.ws
```

The investigation confirmed that the file is a legitimate 64-bit ELF executable with the SUID permission enabled.

---

## Findings

- No Indicators of Compromise (IOCs) were identified.
- No suspicious executable files were found inside `/tmp`.
- SUID binaries appeared consistent with the operating system.
- No evidence of malicious persistence or unauthorized files was observed.

---

## Skills Practiced

- File system investigation
- IOC hunting
- Temporary directory analysis
- Executable file identification
- SUID enumeration
- File validation
- Linux permissions analysis
- Incident investigation methodology
