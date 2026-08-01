# Linux SOC Lab 8 - Incident Correlation

## Objective

The objective of this lab was to perform a complete incident investigation by correlating multiple sources of evidence in a Linux environment.

The investigation focused on identifying possible signs of compromise through:

- Process analysis
- System logs
- Authentication events
- Network connections
- Services
- Scheduled tasks
- Persistence mechanisms

---

# Investigation Process

## 1. Process Investigation

### Commands Used

```bash
top

ps aux
```

### Analysis

The running processes were analyzed to identify:

- High CPU or memory consumption
- Suspicious process names
- Unexpected users executing processes
- Abnormal behavior

### Findings

- No abnormal CPU usage was identified.
- No suspicious processes were found.
- Running processes appeared consistent with the Linux environment.

---

# 2. System Log Analysis

### Command Used

```bash
journalctl -n 50
```

### Analysis

System logs were reviewed to identify:

- Critical errors
- Service failures
- Suspicious system activity

### Findings

- No critical errors were identified.
- Log entries appeared to be normal system activity.

---

# 3. Authentication Investigation

### Command Used

```bash
sudo cat /var/log/auth.log | tail -50
```

### Analysis

Authentication events were reviewed for:

- Failed login attempts
- Invalid users
- Brute force attempts
- Unauthorized privilege escalation

### Findings

- Only expected administrative sessions were identified.
- No failed authentication attempts were observed.
- No unauthorized users were detected.

---

# 4. Network Investigation

### Command Used

```bash
sudo ss -tunap
```

### Analysis

Network connections were reviewed to identify:

- Unknown listening ports
- Suspicious external connections
- Unexpected processes using network resources

### Findings

- Only expected system services were observed.
- No suspicious external connections were identified.
- No unknown network activity was detected.

---

# 5. Persistence Investigation

## Services

### Command Used

```bash
systemctl list-unit-files --state=enabled
```

### Analysis

Enabled services were reviewed to identify unauthorized startup mechanisms.

### Findings

- No suspicious services were found.
- Enabled services were consistent with the operating system.

---

## Cron Jobs

### Commands Used

```bash
crontab -l

ls -la /etc/cron*
```

### Analysis

Scheduled tasks were analyzed to identify possible persistence mechanisms.

### Findings

- No user cron jobs were configured.
- System cron jobs appeared legitimate.
- No malicious scheduled tasks were identified.

---

# Incident Conclusion

After analyzing multiple sources of evidence:

- Processes
- Logs
- Authentication events
- Network activity
- Services
- Scheduled tasks

No Indicators of Compromise (IOCs) were identified.

The system appears to be operating normally, with no evidence of:

- Malware execution
- Unauthorized access
- Suspicious persistence
- Abnormal network activity

---

# Final Assessment

**Severity:** Informational

**Status:** Closed

**Conclusion:**

The investigation did not identify any signs of compromise. All analyzed artifacts were consistent with normal Linux system behavior.

---

# Skills Practiced

- Incident investigation methodology
- Evidence correlation
- Linux process analysis
- Log analysis
- Authentication monitoring
- Network investigation
- Service analysis
- Persistence detection
- SOC analyst workflow
