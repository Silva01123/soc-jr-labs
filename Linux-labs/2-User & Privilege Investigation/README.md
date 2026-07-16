# 🧪 Linux Lab 02 – User & Privilege Investigation

## Objective

Investigate user accounts and administrative privileges on a Linux system to determine whether any unauthorized users or privilege assignments are present.

---

## Scenario

A system administrator reported that a user may have been granted administrative privileges without authorization.

As a SOC Analyst, the objective was to verify user accounts, inspect group memberships, and determine whether any unauthorized privilege escalation had occurred.

---

## Tools & Commands Used

* `cat /etc/passwd`
* `groups`
* `getent group sudo`

---

## Investigation Steps

### 1. User Enumeration

Executed:

```bash
cat /etc/passwd
```

Reviewed:

* Existing user accounts
* System accounts
* Interactive login users

**Result:**

* Standard Linux system accounts were identified.
* The local user `santana` was present.
* No unexpected or suspicious user accounts were found.

---

### 2. User Group Membership

Executed:

```bash
groups
```

Reviewed:

* User group memberships
* Administrative privileges

**Result:**

The user belonged to the following groups:

```text
adm
cdrom
sudo
dip
plugdev
users
```

The presence of the `sudo` group confirms that the user has administrative privileges.

---

### 3. Administrative Group Verification

Executed:

```bash
getent group sudo
```

Reviewed:

* Members of the `sudo` group

**Result:**

```text
sudo:x:27:santana
```

Only the expected user was a member of the administrative group.

---

## Findings

* No unauthorized user accounts were identified.
* No unexpected members of the `sudo` group were found.
* Administrative privileges were assigned only to the expected user.
* No evidence of unauthorized privilege escalation was observed.

---

# Conclusion

The investigation confirmed that the Linux system contained only expected user accounts and administrative group memberships.

Based on the collected evidence, no unauthorized users or privilege assignments were identified, and no indicators of privilege escalation were found.

---

## Skills Demonstrated

* Linux user enumeration
* User account analysis
* Group membership investigation
* Administrative privilege verification
* Linux access control basics
* SOC investigation methodology

