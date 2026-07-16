# 🧪 Linux Lab 03 – Network Investigation

## Objective

Investigate network activity on a Linux system by identifying listening ports, associated services, and active connections to determine whether any unauthorized network activity is present.

---

## Scenario

The monitoring team reported that a Linux host might be exposing an unexpected network service.

As a SOC Analyst, the objective was to identify listening ports, verify the associated processes, inspect active network connections, and determine whether the alert represented a legitimate security incident.

---

## Tools & Commands Used

* `ss -tulpn`
* `ss -tunap`
* `sudo`

---

## Investigation Steps

### 1. Listening Port Enumeration

Executed:

```bash
sudo ss -tulpn
```

Reviewed:

* Listening TCP and UDP ports
* Associated processes
* Local listening addresses

**Observed Services:**

| Port | Protocol | Process            | Purpose                    |
| ---- | -------- | ------------------ | -------------------------- |
| 53   | TCP/UDP  | `systemd-resolved` | DNS Resolver               |
| 323  | UDP      | `chronyd`          | Time Synchronization (NTP) |

**Result:**

Only expected system services were listening on the host.

---

### 2. Service Verification

The identified services were reviewed.

**Findings:**

* `systemd-resolved` is the default Linux DNS resolver.
* `chronyd` is responsible for system time synchronization.
* Most services were bound to loopback addresses (`127.0.0.1`, `127.0.0.53`, `127.0.0.54`), limiting external exposure.

No unauthorized or unexpected services were identified.

---

### 3. Active Connection Analysis

Executed:

```bash
ss -tunap
```

Reviewed:

* Established TCP connections
* UDP activity
* Connection states

**Result:**

* No `ESTAB` (Established) connections were observed.
* UDP sockets appeared in the `UNCONN` state, which is expected for connectionless communication.
* No suspicious external connections were identified.

---

## Findings

* Only legitimate system services were listening on the host.
* No unexpected listening ports were found.
* No active external network connections were established during the investigation.
* No indicators of malicious network activity were identified.

---

# Conclusion

The network investigation confirmed that the Linux host was only exposing expected system services related to DNS resolution and time synchronization.

No suspicious listening ports, unauthorized services, or established external connections were identified. Based on the collected evidence, the reported alert was determined to be a false positive.

---

## Skills Demonstrated

* Linux network investigation
* Listening port analysis
* Service identification
* Active connection analysis
* Network socket interpretation
* Linux service validation
* SOC Analyst investigation methodology

