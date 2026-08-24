# Phase 18 — Windows Telemetry Validation

## Environment

- Domain: enterprise.local
- DC01: 192.168.10.10
- WIN11-CLIENT01: 192.168.10.20
- Host RAM: 15.92 GB
- DC01 VM: 3072 MB RAM, 2 CPUs
- WIN11-CLIENT01 VM: 3072 MB RAM, 2 CPUs
- Kali VM: 2048 MB RAM, 2 CPUs, currently powered off

## Network Validation

- DC01 → WIN11-CLIENT01: PASS
- WIN11-CLIENT01 → DC01: PASS
- WIN11 → DC01 TCP/445: PASS
- DNS resolution of dc01.enterprise.local: PASS

## Sysmon Validation

- Sysmon64 service: Running / Automatic
- Sysmon Operational log: Enabled
- Sysmon Event ID 1 — Process Creation: PASS
- Sysmon Event ID 3 — Network Connection: PASS
- Sysmon Event ID 22 — DNS Query: PASS

## Windows Security Validation

- Security log: Enabled
- Event ID 4624 — Successful Logon: Present
- Event ID 4625 — Failed Logon: Present
- Event ID 4688 — Process Creation: Present

## PowerShell Validation

- PowerShell Operational log: Enabled
- Event ID 4103: Present
- Event ID 4104: Present

## Host Stability Baseline

- Total RAM: 15.92 GB
- Free RAM during latest check: 3.16 GB
- CPU usage during latest check: 8.3%
- DC01: Running
- WIN11-CLIENT01: Running
- Kali: Powered off

## Stability Assessment

The host has approximately 16 GB physical RAM. Running DC01 and WIN11-CLIENT01 together with Chrome, VS Code, and other host applications produces relatively high memory utilization.

CPU usage is currently low, so CPU saturation is not indicated by the baseline.

The current VM configuration should therefore remain unchanged while telemetry validation continues. Kali should remain powered off until additional testing requires it.

## Phase 18 Result

Telemetry validation is successful on WIN11-CLIENT01.

The environment is ready to proceed to the next Phase 18 step.
