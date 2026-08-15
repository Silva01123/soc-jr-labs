🛡️ Linux SOC Investigation — Full Incident Investigation
📌 Overview

This lab simulates a real-world SOC investigation of a Linux endpoint where suspicious activity is suspected.

The objective was to investigate the host from multiple security perspectives, correlate evidence, validate suspicious findings, and determine whether there were sufficient indicators of compromise (IOCs).

The investigation followed a structured SOC workflow:

Identify → Collect Evidence → Investigate → Correlate → Validate → Assess → Conclude

🎯 Investigation Objectives
Identify the current user and privilege level
Investigate running processes
Validate suspicious process executables
Analyze network activity
Review privileged activity and sudo usage
Investigate authentication failures
Identify potential persistence mechanisms
Validate enabled system services
Correlate findings across multiple sources
Determine whether indicators of compromise were present
🔎 Investigation
1. User & Privilege Investigation
Command
whoami
id
Findings

The active user was identified as:

santana
UID: 1000

The account belongs to the sudo group, meaning it has administrative privileges through sudo.

Assessment

The account configuration was consistent with a normal user account with administrative capabilities.

2. Process Investigation
Command
ps aux
Findings

Running processes were reviewed for:

High CPU or memory consumption
Unusual process names
Unexpected privileged processes
Suspicious execution paths

No clearly malicious process was identified.

One process initially requiring validation was:

PID: 9
Process: plan9
User: root
3. Executable Validation
Command
sudo ls -l /proc/9/exe
Result
/proc/9/exe -> /init
Assessment

The executable path was consistent with the WSL environment.

The process was therefore not classified as malicious based on this evidence.

4. Network Investigation
Command
ss -tunap
Findings

Observed services included:

DNS  → Port 53
NTP  → Port 323

The system showed local DNS and NTP listeners, with no suspicious external ESTABLISHED connection identified during the investigation.

Assessment

Network activity was consistent with expected system functionality.

📜 5. Privileged Activity Investigation
Command
journalctl | grep sudo
Findings

The logs contained multiple sudo events, including commands executed by the investigation user.

Examples included:

COMMAND=/usr/bin/whoami
COMMAND=/usr/bin/ss -tulpn
COMMAND=/usr/bin/cat /etc/crontab
COMMAND=/usr/bin/ls -l /proc/9/exe

The commands correlated with activities performed during the investigation and previous security labs.

Assessment

No unexplained privileged command was identified.

🔐 6. Authentication Investigation
Command
sudo grep "Failed password" /var/log/auth.log
Result

No matching Failed password entries were found.

Assessment

No evidence of failed login attempts matching this pattern was identified in the examined authentication log.

Note: sudo authentication failure events were observed separately and were not automatically classified as external login attempts.

🔄 7. Persistence Investigation

Potential persistence mechanisms were reviewed, including:

Cron
Systemd services
Enabled unit files
Socket activation
Executable files in temporary locations
Command
systemctl list-unit-files --state=enabled

Multiple enabled services were identified.

These included expected Linux and WSL-related components such as:

apparmor.service
chrony.service
cron.service
rsyslog.service
systemd-resolved.service
unattended-upgrades.service

No clearly suspicious persistence mechanism was identified.

🔌 8. Socket Activation Investigation

One enabled socket selected for validation was:

snapd.socket
Command
systemctl status snapd.socket
Findings
Active: active (listening)
Triggers: snapd.service
Listen: /run/snapd.socket
        /run/snapd-snap.socket
Assessment

The socket behavior was consistent with normal Snap socket activation.

No suspicious persistence behavior was identified.

🧩 9. Evidence Correlation

The investigation correlated evidence from multiple sources:

Evidence Source	Result
User identity	Expected
User privileges	Expected
Running processes	No clear IOC
Executable paths	Consistent with WSL
Network activity	No suspicious external connection
Sudo activity	Correlated with known activity
Authentication logs	No Failed password detected
Systemd persistence	No suspicious service identified
Socket activation	Expected behavior
🚨 Final Assessment
Result: No Indicators of Compromise Identified

The investigation did not identify sufficient evidence to classify the endpoint as compromised.

Observed activity was consistent with:

Legitimate system processes
Expected WSL functionality
Normal Linux services
Administrative activity performed during the investigation
Expected Snap and systemd behavior

No unexplained process, executable, network connection, privileged command, authentication event, or persistence mechanism was identified as malicious.

🧠 SOC Analyst Takeaways

This investigation reinforced several core SOC skills:

Process investigation
Linux privilege analysis
/proc investigation
Network connection analysis
Authentication log analysis
sudo activity investigation
Persistence hunting
Systemd investigation
Evidence correlation
False-positive reduction
Incident assessment

Most importantly:

A suspicious-looking artifact should not be classified as malicious without validation and contextual correlation.

🛠️ Tools & Commands
System & Identity
whoami
id
Process Investigation
ps aux
top
Process Executable Investigation
sudo ls -l /proc/<PID>/exe
Network Investigation
ss -tunap
Log Investigation
journalctl
journalctl | grep sudo
Authentication Investigation
sudo grep "Failed password" /var/log/auth.log
Persistence Investigation
systemctl list-unit-files --state=enabled
systemctl status <service>
📚 Skills Demonstrated

Linux • SOC Analysis • Incident Investigation • Process Analysis • Network Analysis • Log Analysis • Privilege Investigation • Persistence Hunting • IOC Analysis • Evidence Correlation • False Positive Analysis

🏁 Conclusion

This lab represents a complete Linux endpoint investigation performed from the perspective of a SOC Analyst.

Rather than relying on a single indicator, multiple evidence sources were investigated and correlated before reaching a final assessment.

Final verdict: No evidence of compromise identified
