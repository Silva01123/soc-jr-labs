# 🧪 Linux Lab 01 – Process Investigation

## Objective

Investigate a Linux system reporting performance issues by analyzing running processes, resource usage, executable paths, and network activity to determine whether any suspicious process is present.

---

## Scenario

A system administrator reported that the Linux server was experiencing slowness during the morning. No planned updates or maintenance had been performed, raising the possibility of an unauthorized or resource-intensive process.

As a SOC Analyst, the objective was to investigate the running processes and determine whether the system showed any signs of malicious activity.

---

## Tools & Commands Used

* `top`
* `ps aux`
* `grep`
* `ls -l /proc/<PID>/exe`
* `ss -tulpn`
* `sudo`

---

## Investigation Steps

### 1. Real-Time Process Analysis

Used the `top` command to monitor CPU and memory usage in real time.

**Result:**

* No process showed abnormal CPU utilization.
* Memory usage appeared normal.
* No indication that resource consumption was causing the reported slowness.

---

### 2. Running Process Enumeration

Executed:

```bash
ps aux
```

Reviewed:

* Running processes
* Process owners
* CPU and memory usage
* Executable commands

**Result:**

No unusual process names, users, or abnormal resource consumption were identified.

---

### 3. Executable Path Verification

Filtered Python processes:

```bash
ps aux | grep python3
```

Verified the executable location:

```bash
sudo ls -l /proc/<PID>/exe
```

**Result:**

The investigated process was executing from:

```text
/usr/bin/python3.14
```

The executable was located in a legitimate system directory.

---

### 4. Network Service Inspection

Executed:

```bash
sudo ss -tulpn
```

Reviewed:

* Listening ports
* Associated processes
* Local services
* Active network listeners

**Observed Services:**

* `systemd-resolved` (DNS - Port 53)
* `chronyd` (Time Synchronization - Port 323)

No suspicious listening services or unexpected network activity were identified.

---

## Findings

* No suspicious running processes.
* No abnormal CPU or memory usage.
* Executables located in legitimate system directories.
* Expected system services were listening on standard ports.
* No indicators of malicious activity were observed during the investigation.

---

# Conclusion

The Linux system was successfully investigated using process enumeration, executable verification, and network analysis.

Based on the collected evidence, no suspicious processes, unauthorized executables, or abnormal network services were identified. The reported slowness could not be reproduced during the investigation, and no indicators of compromise (IOCs) were found.

---

## Skills Demonstrated

* Linux process investigation
* Resource monitoring
* Process filtering with `grep`
* Executable path verification
* Network service analysis
* Basic Linux incident investigation
* SOC Analyst methodology

