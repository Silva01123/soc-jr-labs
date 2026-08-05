# Linux SOC Lab 9 - Incident Response Simulation

## Objective

The objective of this lab was to simulate a real SOC incident response workflow by investigating a Linux system after receiving an alert of suspicious activity.

The goal was to collect evidence, validate findings, eliminate false positives, and determine whether the system had been compromised.

---

# Scenario

A monitoring system generated the following alert:

> **Alert: Suspicious activity detected on Linux server.**

Possible concerns included:

- Suspicious process execution
- Unauthorized persistence
- Abnormal system activity

As a SOC Analyst, the objective was to investigate the alert and determine whether the system was compromised.

---

# Investigation Process

## 1. User and Privilege Verification

### Commands Used

```bash
whoami

id
```

### Analysis

The current user and privilege level were verified before starting the investigation.

### Findings

- Current user: **santana**
- User ID (UID): **1000**
- Member of the **sudo** group
- No abnormal privileges identified

---

# 2. Process Investigation

### Commands Used

```bash
top

ps aux
```

### Analysis

Running processes were reviewed to identify:

- High CPU usage
- High memory usage
- Unknown process names
- Unexpected running services

One process initially attracted attention due to having the highest CPU usage.

```
PID 1
COMMAND: /sbin/init
USER: root
```

The executable and process information were reviewed to validate its legitimacy.

### Findings

- The process was identified as the Linux init process.
- Executed by the **root** user.
- CPU usage was low and consistent with normal system operation.
- No suspicious processes were identified.

---

# 3. Persistence Investigation

## Enabled Services

### Command Used

```bash
systemctl list-unit-files --state=enabled
```

### Analysis

Enabled services were reviewed to identify unauthorized startup mechanisms.

### Findings

- Only expected Linux services were enabled.
- No unknown or suspicious services were identified.

---

## User Cron Jobs

### Command Used

```bash
crontab -l
```

### Findings

- No user cron jobs were configured.

---

## System Cron Jobs

### Commands Used

```bash
ls -la /etc/cron*

sudo cat /etc/crontab
```

### Analysis

System scheduled tasks were reviewed for possible persistence mechanisms.

### Findings

- Only default Ubuntu scheduled tasks were identified.
- No malicious or unauthorized cron jobs were found.

---

# Investigation Summary

The following artifacts were analyzed:

- User privileges
- Running processes
- CPU utilization
- Enabled services
- User cron jobs
- System cron jobs

No Indicators of Compromise (IOCs) were identified during the investigation.

---

# Final Assessment

**Severity:** Informational

**Status:** Closed

**Conclusion:**

The investigation did not identify evidence of malicious activity or unauthorized persistence.

All observed processes, services, and scheduled tasks were consistent with normal Linux system behavior.

The alert was determined to be a false positive, and no further response actions were required.

---

# Skills Practiced

- Incident response methodology
- Linux process analysis
- CPU and memory monitoring
- Privilege verification
- Persistence investigation
- Service analysis
- Scheduled task analysis
- False positive validation
- Evidence-based decision making
- SOC investigation workflow
