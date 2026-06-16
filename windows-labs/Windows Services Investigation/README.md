# Windows Services Investigation Lab

## Objective

Investigate Windows services, identify running services, and correlate them with system processes.

## Tools Used

- PowerShell
- CMD
- Get-Service
- tasklist /svc

## Investigation

Running services were identified using PowerShell.

The BFE (Base Filtering Engine) service was selected for investigation.

The service status was verified and confirmed as running.

The service was then correlated with its hosting process using tasklist /svc.

The investigation confirmed that the BFE service was running under svchost.exe with PID 5240.

Additional analysis identified that the same process was hosting the Windows Firewall service (mpssvc).

## Results

- BFE service identified and validated.
- Service status confirmed as running.
- Process correlation completed.
- svchost.exe (PID 5240) was hosting BFE and mpssvc.
- Relationship between Windows services and system processes successfully demonstrated.

## Conclusion

A Windows service investigation was successfully performed using PowerShell and CMD.

The investigation demonstrated how Windows services operate under svchost.exe and how service-to-process correlation can be performed during security investigations.

No suspicious services were identified.
