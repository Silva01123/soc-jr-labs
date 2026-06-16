# Lab 1-Process Investigation Lab

## Objective
Investigate running Windows processes and identify suspicious behavior.

## Tools Used
- Task Manager
- CMD
- tasklist
- netstat -ano
- PowerShell
- Get-Process

## Investigation
- Analyzed running processes and memory usage.
- Investigated chrome.exe and svchost.exe activity.
- Validated ctfmon.exe legitimacy through System32 path verification.
- Correlated active connections with process IDs using netstat.

## Findings
- Chrome multi-process activity identified as normal behavior.
- svchost.exe processes identified as legitimate Windows services.
- ctfmon.exe validated as legitimate.
- No suspicious activity identified.

## Conclusion
Basic Windows process investigation completed successfully using CMD, PowerShell, and Task Manager.
