# 🧪 Linux Lab 05 – Persistence Investigation

## Objective

Investigate a Linux system for persistence mechanisms by reviewing active services, scheduled tasks, and system-wide cron configurations to identify potential unauthorized persistence.

---

## Scenario

The Incident Response team suspected that an attacker might have established persistence on a Linux server to regain access after a reboot.

As a SOC Analyst, the objective was to investigate common persistence locations and determine whether any unauthorized services or scheduled tasks were present.

---

## Tools & Commands Used

* `systemctl list-units --type=service`
* `crontab -l`
* `ls -la /etc/cron*`
* `sudo cat /etc/crontab`

---

## Investigation Steps

### 1. Service Enumeration

Executed:

```bash
systemctl list-units --type=service
```

Reviewed:

* Running services
* Automatically managed services
* Service names that could indicate persistence

**Result:**

Only legitimate Ubuntu services were identified, including:

* `chrony.service`
* `cron.service`
* `dbus.service`
* `networkd-dispatcher.service`
* `rsyslog.service`
* `systemd-journald.service`
* `systemd-logind.service`
* `systemd-resolved.service`
* `systemd-udevd.service`
* `user@1000.service`

The environment also contained `wsl-pro.service`, which is expected when running Ubuntu under Windows Subsystem for Linux (WSL).

No suspicious or unknown services were identified.

---

### 2. User Cron Jobs

Executed:

```bash
crontab -l
```

Output:

```text
no crontab for santana
```

**Result:**

No scheduled cron jobs were configured for the current user.

---

### 3. System Cron Directories

Executed:

```bash
ls -la /etc/cron*
```

Reviewed:

* `/etc/cron.d`
* `/etc/cron.daily`
* `/etc/cron.hourly`
* `/etc/cron.weekly`
* `/etc/cron.monthly`
* `/etc/cron.yearly`

Observed scheduled maintenance tasks included:

* `apport`
* `apt-compat`
* `dpkg`
* `logrotate`
* `man-db`
* `e2scrub_all`

All identified tasks were legitimate Ubuntu maintenance jobs.

No suspicious scripts or unknown scheduled tasks were found.

---

### 4. Global Crontab Review

Executed:

```bash
sudo cat /etc/crontab
```

Reviewed:

* System-wide scheduled tasks
* Scheduled execution times
* Commands executed as `root`

Observed scheduled tasks:

* Hourly execution of `/etc/cron.hourly`
* Daily execution of `/etc/cron.daily`
* Weekly execution of `/etc/cron.weekly`
* Monthly execution of `/etc/cron.monthly`

All entries matched the default Ubuntu configuration.

No unauthorized commands or persistence mechanisms were identified.

---

## Findings

* No suspicious services were found.
* No user cron jobs were configured.
* System cron directories contained only legitimate maintenance scripts.
* The global crontab contained only default Ubuntu scheduled tasks.
* No indicators of persistence were identified.

---

# Conclusion

A persistence investigation was performed by reviewing active services, user cron jobs, system cron directories, and the global crontab configuration.

All identified services and scheduled tasks were consistent with a standard Ubuntu installation running in a WSL environment.

No evidence of unauthorized persistence mechanisms or malicious scheduled tasks was identified.

---

## Skills Demonstrated

* Linux persistence investigation
* Service analysis
* Cron job investigation
* System-wide scheduled task analysis
* Linux incident response
* Security log interpretation
* SOC Analyst investigation methodology

