# Enterprise SOC Lab

A hands-on enterprise Security Operations Center lab built to demonstrate practical experience in:

- SOC monitoring
- Active Directory
- Wazuh SIEM
- Sysmon telemetry
- Detection engineering
- MITRE ATT&CK mapping
- Attack simulation
- Threat hunting
- Incident response
- False-positive investigation
- Windows security monitoring

The project simulates a small enterprise environment where security telemetry is generated, collected, analyzed, investigated, and documented through a structured SOC workflow.

---

## Project Objective

The objective of this project is to build a realistic enterprise cybersecurity lab that demonstrates the complete security monitoring lifecycle:

1. Design an enterprise environment.
2. Deploy Windows and Linux systems.
3. Configure Active Directory.
4. Deploy endpoint telemetry.
5. Centralize logs using Wazuh.
6. Simulate attacker and suspicious activity.
7. Develop and test detection rules.
8. Investigate alerts.
9. Perform threat hunting.
10. Conduct incident-response analysis.
11. Document findings and lessons learned.

---

## Lab Architecture

The environment consists of four primary systems:

| System | Operating System | Role |
|---|---|---|
| DC01 | Windows Server 2022 | Active Directory, DNS, Authentication |
| WIN11-CLIENT01 | Windows 11 | Enterprise workstation, Sysmon, Wazuh Agent |
| WAZUH01 | Amazon Linux 2023 | Wazuh Manager and centralized security monitoring |
| KALI01 | Kali Linux | Controlled attack simulation |

Primary enterprise network:

`192.168.10.0/24`

Key systems:

- DC01: `192.168.10.10`
- WIN11-CLIENT01: `192.168.10.20`
- WAZUH01: `192.168.10.30`

The lab uses an isolated VirtualBox network to safely generate and analyze security activity.

---

## Core Technologies

### Security Monitoring

- Wazuh SIEM
- Sysmon
- Windows Event Logs
- PowerShell Operational Logs
- Wazuh custom rules
- Wazuh Dashboard

### Windows Infrastructure

- Windows Server 2022
- Active Directory Domain Services
- DNS
- Organizational Units
- Security Groups
- Group Membership
- Security Policies
- Windows Auditing
- Windows 11 domain integration

### Detection & Investigation

- MITRE ATT&CK
- Detection engineering
- Custom Wazuh rules
- Alert triage
- Threat hunting
- Process validation
- Network investigation
- File hash analysis
- Authenticode signature validation
- False-positive analysis

### Attack Simulation

- Kali Linux
- Controlled network activity
- SMB enumeration testing
- PowerShell-generated telemetry
- Sysmon network events
- File creation events
- DNS telemetry

---

## Security Telemetry

The Windows endpoint collects and forwards security telemetry including:

- Windows Security Events
- Windows System Events
- Windows Application Events
- Sysmon Operational Events
- PowerShell Operational Events

Important telemetry validated during the project includes:

- Windows Security Event ID 4688
- PowerShell Event ID 4104
- Sysmon Event ID 3 - Network Connection
- Sysmon Event ID 11 - File Creation
- Sysmon Event ID 22 - DNS Query

The Wazuh Agent on WIN11-CLIENT01 forwards events to the centralized Wazuh Manager for monitoring and investigation.

---

## Detection Engineering

Detection engineering was performed using Wazuh and Sysmon telemetry.

One Phase 19 detection focused on:

**MITRE ATT&CK T1046 - Network Service Discovery**

A custom Wazuh rule was created to detect Sysmon network activity.

The initial rule successfully generated alerts but was found to be overly broad.

During validation, legitimate Wazuh Agent traffic was detected as suspicious activity.

Example communication:

`WIN11-CLIENT01 -> WAZUH01:1514/TCP`

Process:

`wazuh-agent.exe`

This became the basis for the Phase 20 SOC investigation.

---

## Incident Response Investigation

Phase 20 demonstrated the full SOC investigation workflow.

The alert investigated was:

- MITRE Technique: T1046 - Network Service Discovery
- Wazuh Rule ID: 100100
- Rule Level: 8
- Endpoint: WIN11-CLIENT01
- Process: wazuh-agent.exe
- PID: 2240
- Destination: 192.168.10.30:1514/TCP

The investigation validated:

- Wazuh Agent service status
- Agent connectivity
- Process path
- Process ID
- Network destination
- Wazuh Manager listening service
- SHA256 file hash
- Authenticode signature
- Similar activity through threat hunting

SHA256 examined:

`7C98FE80900087FF12CC629842ED9D62754AFF65E81CF7790BA09984B7A64B4D`

The process was confirmed to be legitimate Wazuh Agent activity.

Final incident classification:

**FALSE POSITIVE**

Final incident status:

**CLOSED - FALSE POSITIVE**

The root cause was an overly broad detection rule rather than malicious activity.

---

## Detection Engineering Lesson

This project demonstrates an important SOC principle:

> A security alert is not automatically a security incident.

Detection rules must be tested against legitimate infrastructure behavior.

The Phase 19 and Phase 20 workflow demonstrated:

`Telemetry -> Detection -> Alert -> Investigation -> False Positive -> Detection Tuning`

This reflects the continuous improvement cycle used in real SOC environments.

---

## Project Phases

| Phase | Description | Status |
|---|---|---|
| 01 | Project Planning & Repository Initialization | Complete |
| 02 | Infrastructure Planning | Complete |
| 03 | Virtualization Platform Setup | Complete |
| 04 | Windows Server Deployment | Complete |
| 05 | Active Directory Deployment | Complete |
| 06 | Enterprise Environment Overview | Complete |
| 07 | Active Directory Architecture & Implementation | Complete |
| 08 | Enterprise Network Architecture | Complete |
| 09 | Security Operations Center Design | Complete |
| 10 | Detection Engineering | Complete |
| 11 | Windows Server Rebuild & Domain Controller Promotion | Complete |
| 12 | Organizational Unit Design | Complete |
| 13 | Security Groups | Complete |
| 14 | Active Directory Group Membership | Complete |
| 15 | Security Policies & Auditing | Complete |
| 16 | Windows 11 Domain Join | Complete |
| 17 | Kali Linux Attacker Setup | Complete |
| 18 | Wazuh SIEM Deployment & Log Collection | Complete |
| 19 | Attack Simulation & Detection Engineering | Complete |
| 20 | Incident Response & SOC Investigation | Complete |
| 21 | Final Documentation, Validation & Release | Complete |

---

## Current Status

**Project Status: COMPLETE**

All 21 phases of the Enterprise SOC Lab have been successfully completed.

The project now includes enterprise infrastructure design, Active Directory, Windows endpoint monitoring, Sysmon telemetry, Wazuh SIEM, detection engineering, MITRE ATT&CK mapping, controlled attack simulation, threat hunting, incident response, false-positive investigation, technical documentation, and supporting evidence.

The repository has completed its final documentation, validation, cleanup, and release process.

## Repository Structure

```text
ENTERPRISE-SOC-LAB/
|
+-- active-directory/
+-- architecture/
+-- assets/
+-- attack-scenarios/
+-- dashboards/
+-- detection-rules/
+-- diagrams/
+-- docs/
+-- elastic/
+-- incident-response/
+-- infrastructure/
+-- installation/
+-- linux/
+-- network/
+-- reports/
+-- screenshots/
+-- sigma/
+-- SOC/
+-- threat-hunting/
+-- wazuh/
+-- windows/
|
+-- README.md
+-- ROADMAP.md
+-- CHANGELOG.md
+-- CONTRIBUTING.md
+-- LICENSE