🧪 Linux Lab 6 – Service Investigation

Objective

Investigate a Linux service to determine whether it is legitimate by analyzing its status, startup configuration, running process, and executable path.

---

Scenario

A monitoring system generated an alert related to the **networkd-dispatcher** service. The objective was to verify whether the service had been modified or if it was a legitimate system component.

---

 Investigation Steps

### 1. Check the service status

```bash
systemctl status networkd-dispatcher.service
```

**Result:**

- Service loaded successfully.
- Service enabled to start automatically.
- Service active and running.
- Main PID identified.
- Startup command displayed.

---

### 2. Identify the main process

From the previous command:

```
Main PID: 140
```

The service was running as:

```
/usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
```

---

### 3. Verify the executable

```bash
sudo ls -l /proc/140/exe
```

**Result:**

```
/proc/140/exe -> /usr/bin/python3.14
```

This confirms that the running process is using the expected Python interpreter.

---

## Analysis

The investigation confirmed that:

- The service is installed correctly.
- The service starts automatically.
- The service is currently running.
- The executable path is legitimate.
- The process matches the expected startup configuration.
- No indicators of compromise (IOCs) were identified.

---

## Conclusion

The **networkd-dispatcher** service is a legitimate Ubuntu system service responsible for reacting to network state changes. The executable path, process information, and startup configuration were consistent with expected system behavior.

**Status:** ✅ Legitimate service – No suspicious activity identified.
