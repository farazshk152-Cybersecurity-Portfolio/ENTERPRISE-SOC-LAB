# 🛡️ Enterprise SOC Lab

![Status](https://img.shields.io/badge/Project-Complete-brightgreen)
![Phases](https://img.shields.io/badge/Phases-22%2F22-brightgreen)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh-blue)
![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-red)

## Enterprise Security Monitoring, Detection Engineering & Incident Response Lab

The **Enterprise SOC Lab** is a hands-on cybersecurity project designed to simulate a small enterprise environment and demonstrate practical Security Operations Center (SOC) workflows.

The project was built from the ground up using Windows Server, Active Directory, Windows 11, Sysmon, PowerShell logging, Wazuh SIEM, Kali Linux, MITRE ATT&CK, detection engineering, controlled attack simulation, threat investigation, false-positive analysis, true-positive validation, and incident-response documentation.

Rather than functioning as a basic SIEM installation, the lab demonstrates the complete security monitoring lifecycle:

**Infrastructure → Endpoint Telemetry → Centralized Logging → Detection → Investigation → Classification → Response → Documentation**

The project contains **22 completed phases** and includes both a verified **False Positive investigation** and a verified **True Positive investigation**.

---

# 📌 Project Status

**Status: COMPLETE ✅**

**Completed Phases: 22 / 22**

The Enterprise SOC Lab has successfully demonstrated:

- Enterprise network design
- Virtualized security infrastructure
- Windows Server deployment
- Active Directory
- Organizational Units and security groups
- Windows domain integration
- Windows security auditing
- Sysmon endpoint telemetry
- PowerShell Script Block Logging
- Wazuh SIEM deployment
- Centralized Windows log collection
- Detection engineering
- MITRE ATT&CK mapping
- Controlled attack simulation
- Alert triage
- False Positive investigation
- True Positive investigation
- Process and file investigation
- Threat hunting
- Incident-response workflow
- Evidence collection
- SOC documentation
- Detection tuning analysis
- Post-investigation validation

---

# 🎯 Project Objectives

The main objective of this project was to build a realistic enterprise-style SOC laboratory capable of demonstrating practical blue-team and security operations skills.

The project was designed to answer questions such as:

- How are enterprise endpoints monitored?
- How does Windows generate security telemetry?
- How does Sysmon improve endpoint visibility?
- How can PowerShell activity be monitored?
- How are endpoint logs forwarded to a SIEM?
- How does Wazuh process Windows security events?
- How are security detections mapped to MITRE ATT&CK?
- How are controlled attack simulations validated?
- How does a SOC analyst investigate an alert?
- How can a False Positive be distinguished from a True Positive?
- How should detection rules be tuned?
- How should investigation evidence be documented?
- How can endpoint, SIEM, and analyst evidence be correlated?

---

# 🏗️ Lab Architecture

The Enterprise SOC Lab uses a segmented virtual environment built with **Oracle VirtualBox**.

## Enterprise Network

```text
192.168.10.0/24
```

Core systems used throughout the project include:

| System | Role | Enterprise IP |
|---|---|---:|
| DC01 | Windows Server / Active Directory / DNS | 192.168.10.10 |
| WIN11-CLIENT01 | Windows 11 monitored endpoint | 192.168.10.20 |
| WAZUH01 | Wazuh SIEM Manager | 192.168.10.30 |
| Kali Linux | Controlled attack simulation system | Lab network / staged operation |

The environment was operated using staged VM execution to control host resource usage.

---

# 🖥️ Core Infrastructure

## DC01

DC01 provides the enterprise identity and domain infrastructure.

Functions include:

- Active Directory Domain Services
- DNS
- Domain Controller functionality
- Organizational Unit structure
- Security groups
- Group membership
- Security policy configuration
- Windows auditing
- Domain authentication

Enterprise IP:

```text
192.168.10.10
```

---

## WIN11-CLIENT01

WIN11-CLIENT01 serves as the primary monitored Windows endpoint.

Enterprise IP:

```text
192.168.10.20
```

The endpoint was integrated with:

- Active Directory
- Windows Security auditing
- Sysmon
- PowerShell Operational Logging
- PowerShell Script Block Logging
- Wazuh Agent

Wazuh Agent:

```text
Agent ID: 002
Agent Name: WIN11-CLIENT01
Status: Active
```

The endpoint also used a VirtualBox NAT interface where required for external connectivity.

---

## WAZUH01

WAZUH01 provides centralized SIEM functionality.

Operating System:

```text
Amazon Linux 2023
```

Enterprise IP:

```text
192.168.10.30
```

Wazuh was used for:

- Agent management
- Windows log collection
- Event decoding
- Detection rules
- Alert generation
- MITRE ATT&CK mapping
- Investigation
- Threat hunting
- Detection validation

---

## Kali Linux

Kali Linux was used only for authorized controlled security testing inside the isolated lab environment.

Activities included controlled:

- Connectivity testing
- Service discovery
- SMB enumeration testing
- Network discovery
- Detection validation

No destructive attack activity was required for the project.

---

# 🔄 Security Telemetry Flow

The core monitoring architecture can be represented as:

```text
+-------------------------+
|     Windows Endpoint    |
|    WIN11-CLIENT01       |
|     192.168.10.20       |
+------------+------------+
             |
             | Security Events
             | Sysmon Events
             | PowerShell Events
             v
+-------------------------+
|       Wazuh Agent       |
|        Agent 002        |
+------------+------------+
             |
             | Centralized Event Forwarding
             v
+-------------------------+
|       WAZUH01           |
|      Wazuh Manager      |
|     192.168.10.30       |
+------------+------------+
             |
             | Decode
             | Rules
             | Correlation
             | MITRE Mapping
             v
+-------------------------+
|     Wazuh Dashboard     |
|   Alerts / Investigation|
+------------+------------+
             |
             v
+-------------------------+
|       SOC Analyst       |
| Triage / Investigation  |
| TP / FP Classification  |
| Response / Documentation|
+-------------------------+
```

---

# 🔍 Endpoint Telemetry

A major part of the project focused on generating and validating useful Windows endpoint telemetry.

## Windows Security Logging

Windows Security auditing was configured and validated.

Centralized evidence included:

```text
Event ID 4688
```

This provides visibility into Windows process creation activity.

---

# 🔬 Sysmon

Sysmon was deployed to provide enhanced Windows endpoint visibility.

Version used:

```text
Sysmon 15.21
```

Important Sysmon events observed during the project included:

| Event ID | Purpose |
|---:|---|
| 3 | Network Connection |
| 11 | File Create |
| 22 | DNS Query |

Sysmon Event ID 11 was successfully verified centrally through Wazuh telemetry.

A key lesson from this work was that:

> Event ingestion and alert generation are not the same thing.

An event can successfully reach the SIEM without generating a visible alert if the associated rule is non-alerting or level 0.

---

# ⚡ PowerShell Monitoring

PowerShell Operational Logging was integrated into the monitoring pipeline.

A particularly important event used in the project was:

```text
PowerShell Event ID 4104
```

Event ID 4104 provides **PowerShell Script Block Logging**, allowing analysts to inspect PowerShell content executed on an endpoint.

This telemetry later became the foundation for the project's verified True Positive investigation.

---

# 🛡️ Wazuh SIEM Integration

The Windows endpoint was integrated with Wazuh using:

```text
C:\Program Files (x86)\ossec-agent\
```

Wazuh service:

```text
WazuhSvc
```

The following Windows channels were integrated:

```text
Application
Security
System
Microsoft-Windows-Sysmon/Operational
Microsoft-Windows-PowerShell/Operational
```

Centralized monitoring successfully validated:

- Windows Security Event 4688
- PowerShell Event 4104
- Sysmon telemetry
- Endpoint-to-manager communication
- Wazuh detection rules
- MITRE ATT&CK mapping

---

# 🧩 Wazuh Troubleshooting & Recovery

The project also included real SIEM troubleshooting rather than only successful configurations.

During integration, a malformed custom decoder caused:

```text
wazuh-analysisd
```

validation/startup problems.

The malformed decoder was backed up and disabled rather than blindly deleted.

Configuration validation was performed using:

```bash
/var/ossec/bin/wazuh-analysisd -t
```

After correction:

- Analysis configuration validated successfully
- Wazuh Manager services recovered
- Ports 1514/1515 returned
- Agent 002 reconnected
- Windows telemetry collection resumed

This demonstrated practical troubleshooting of a SIEM configuration failure.

---

# 🧠 Detection Engineering

The project progressed beyond log collection into detection engineering.

Controlled activities were generated and then followed through the telemetry pipeline.

The detection-engineering workflow used throughout the project was:

```text
Generate Activity
      ↓
Verify Endpoint Telemetry
      ↓
Verify Central Ingestion
      ↓
Analyze Wazuh Rule Behavior
      ↓
Map to MITRE ATT&CK
      ↓
Investigate Alert
      ↓
Identify False Positives / True Positives
      ↓
Tune Detection
```

---

# 🎯 MITRE ATT&CK

MITRE ATT&CK was used to map observed security behavior to standardized adversary techniques.

Important techniques investigated during the project include:

| Technique | ID | Purpose |
|---|---|---|
| Network Service Discovery | T1046 | Discover network services |
| Network Share Discovery | T1135 | Discover shared network resources |
| Process Discovery | T1057 | Discover running processes |
| PowerShell | T1059.001 | PowerShell execution context |

Not every simulated technique resulted in a successful detection.

Unsuccessful or blocked tests were documented honestly rather than represented as successful attacks.

---

# 🧪 Controlled Attack Simulation

The lab used controlled and authorized security activity to validate monitoring capabilities.

Examples included:

- Network connectivity testing
- SMB enumeration
- Service discovery
- PowerShell activity
- Sysmon network activity
- Process Discovery
- File creation
- DNS activity

All testing occurred within the lab environment.

---

# 🔎 Phase 19 — Detection Engineering

Phase 19 focused heavily on **T1046 — Network Service Discovery**.

A controlled PowerShell connection test generated Sysmon Event ID 3 telemetry.

The observed communication included:

```text
WIN11-CLIENT01
192.168.10.20

        ↓

WAZUH01
192.168.10.30
Port 55000
```

The telemetry successfully reached Wazuh.

Native Sysmon Event 3 processing involved Wazuh rule:

```text
61605
```

which was non-alerting at level 0.

---

## Experimental T1046 Detection

A custom detection rule was tested:

```text
Rule ID: 100100
Level: 8
MITRE: T1046
```

The rule successfully generated alerts.

However, investigation revealed that it was too broad.

It matched legitimate:

```text
wazuh-agent.exe
```

network communication to Wazuh infrastructure.

This created a useful real-world detection engineering problem:

```text
Detection works
      ↓
Alert generated
      ↓
Analyst investigates
      ↓
Legitimate behavior discovered
      ↓
False Positive identified
      ↓
Rule requires tuning
```

A narrower experimental rule was later evaluated but did not generate the intended alert and was safely disabled.

The project does not claim that unsuccessful rule attempt as a successful detection.

---

# 🚨 Phase 20 — Incident Response & False Positive Investigation

Phase 20 transformed the Phase 19 alert into a complete SOC investigation.

The selected alert was:

```text
Rule ID: 100100
Rule Level: 8
MITRE ATT&CK: T1046
Technique: Network Service Discovery
```

Affected endpoint:

```text
WIN11-CLIENT01
192.168.10.20
Agent 002
```

Observed process:

```text
C:\Program Files (x86)\ossec-agent\wazuh-agent.exe
```

Observed connection:

```text
192.168.10.20:55410
        ↓
192.168.10.30:1514/TCP
```

The investigation verified that Wazuh legitimately listens on port:

```text
1514
```

The endpoint Wazuh service was running normally.

The process path was consistent with the installed Wazuh Agent.

SHA-256:

```text
7C98FE80900087FF12CC629842ED9D62754AFF65E81CF7790BA09984B7A64B4D
```

Authenticode signature:

```text
Valid
```

Threat hunting found only the expected Wazuh Agent communication associated with the alerts.

---

## Phase 20 Classification

Final classification:

```text
FALSE POSITIVE
```

Analyst assessment:

```text
Benign / Expected Activity
```

Root cause:

```text
Overly broad custom detection rule
```

Response:

```text
Host Isolation:      No
Process Termination: No
Credential Reset:    No
Escalation:          No
```

Incident status:

```text
CLOSED — FALSE POSITIVE
```

This phase demonstrated that SOC analysts should never assume an alert represents malicious activity simply because it has a MITRE ATT&CK mapping or elevated rule level.

---

# 🔴 Phase 22 — True Positive Detection & Investigation

Phase 22 was added to demonstrate the opposite alert-classification outcome.

A controlled PowerShell Process Discovery activity was executed on WIN11-CLIENT01:

```powershell
Get-Process | Select-Object -First 10
```

This behavior maps to:

```text
MITRE ATT&CK: T1057
Technique: Process Discovery
Tactic: Discovery
```

---

## Endpoint Evidence

PowerShell Script Block Logging captured the exact activity.

```text
Event ID: 4104
TimeCreated: 07-09-2026 15:29:20
```

Captured script block:

```powershell
Get-Process | Select-Object -First 10
```

ScriptBlock ID:

```text
e0f674bf-d513-4b26-a6d5-1b625fd6e810
```

This proved that Process Discovery actually occurred on the endpoint.

---

## Wazuh Detection

Wazuh generated the corresponding alert:

```text
Agent ID:        002
Agent Name:      WIN11-CLIENT01
Agent IP:        192.168.10.20

Rule ID:         91815
Rule Level:      4
Rule Description:
Powershell executing process discovery

Windows Event:   4104

MITRE ID:        T1057
Tactic:          Discovery
Technique:       Process Discovery
```

The Wazuh alert contained the controlled `Get-Process` script block, providing direct correlation between the endpoint activity and SIEM detection.

---

## Process Investigation

PowerShell executable:

```text
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
```

SHA-256 observed during investigation:

```text
7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5
```

Authenticode signature:

```text
Valid
```

The legitimate signed PowerShell executable was used to perform security-relevant Process Discovery behavior.

This demonstrates an important SOC principle:

> A legitimate executable does not automatically mean the behavior performed through that executable is benign.

---

## Phase 22 Classification

Final classification:

```text
TRUE POSITIVE
```

Context:

```text
Authorized Controlled Security Test
```

The alert was classified as a True Positive because:

1. Process Discovery actually occurred.
2. The analyst intentionally executed the activity.
3. Windows captured the exact command in Event ID 4104.
4. Wazuh received and processed the telemetry.
5. Wazuh Rule 91815 detected Process Discovery.
6. The alert mapped correctly to MITRE ATT&CK T1057.
7. The detected behavior matched the behavior actually performed.

Because the activity was authorized laboratory testing:

```text
Host Isolation:      Not required
Process Termination: Not required
Credential Reset:    Not required
Network Containment: Not required
Escalation:          Not required
```

Post-investigation validation confirmed:

```text
Agent 002
WIN11-CLIENT01
192.168.10.20
Status: Active
```

---

# ⚖️ False Positive vs True Positive

One of the strongest outcomes of the Enterprise SOC Lab is that it demonstrates both alert classifications.

| Investigation | Detection | Result |
|---|---|---|
| Phase 20 | T1046 Network Service Discovery | ❌ False Positive |
| Phase 22 | T1057 Process Discovery | ✅ True Positive |

## False Positive

Phase 20 demonstrated that an alert can appear suspicious while investigation proves the underlying activity is legitimate.

```text
T1046 Alert
    ↓
Investigate process
    ↓
wazuh-agent.exe
    ↓
Legitimate Wazuh communication
    ↓
FALSE POSITIVE
```

## True Positive

Phase 22 demonstrated that a detection can correctly identify behavior that actually occurred.

```text
Get-Process
    ↓
PowerShell Event 4104
    ↓
Wazuh Agent 002
    ↓
Rule 91815
    ↓
MITRE T1057
    ↓
Analyst correlation
    ↓
TRUE POSITIVE
```

Together, these investigations demonstrate practical alert triage rather than simply generating alerts.

---

# 🧯 Incident Response Workflow

The project demonstrates the following SOC investigation methodology:

```text
Alert Generated
      ↓
Initial Triage
      ↓
Identify Endpoint
      ↓
Identify User / Process
      ↓
Inspect Command / Activity
      ↓
Inspect File / Hash / Signature
      ↓
Analyze Network Indicators
      ↓
MITRE ATT&CK Mapping
      ↓
Determine Severity
      ↓
Threat Hunt
      ↓
Build Timeline
      ↓
Classify TP / FP
      ↓
Containment Decision
      ↓
Remediation Decision
      ↓
Recovery / Validation
      ↓
Lessons Learned
      ↓
Incident Closure
```

Not every investigation requires containment.

Response actions should be based on evidence and context.

---

# 📊 Project Phases

| Phase | Description | Status |
|---:|---|:---:|
| 01 | Project Planning & Repository Initialization | ✅ Complete |
| 02 | Infrastructure Planning | ✅ Complete |
| 03 | Virtualization Platform Setup | ✅ Complete |
| 04 | Windows Server Deployment | ✅ Complete |
| 05 | Active Directory Deployment | ✅ Complete |
| 06 | Enterprise Environment Overview | ✅ Complete |
| 07 | Active Directory Architecture & Implementation | ✅ Complete |
| 08 | Enterprise Network Architecture | ✅ Complete |
| 09 | Security Operations Center Design | ✅ Complete |
| 10 | Detection Engineering | ✅ Complete |
| 11 | Windows Server Rebuild & Domain Controller Promotion | ✅ Complete |
| 12 | Organizational Unit Design | ✅ Complete |
| 13 | Security Groups | ✅ Complete |
| 14 | Active Directory Group Membership | ✅ Complete |
| 15 | Security Policies & Auditing | ✅ Complete |
| 16 | Windows 11 Domain Join | ✅ Complete |
| 17 | Controlled Attack Simulation & Sysmon Validation | ✅ Complete |
| 18 | Wazuh SIEM Deployment & Log Collection | ✅ Complete |
| 19 | Attack Simulation & Detection Engineering | ✅ Complete |
| 20 | Incident Response & SOC Investigation | ✅ Complete |
| 21 | Final Documentation, Validation & Repository Release | ✅ Complete |
| 22 | True Positive Detection & Incident Investigation | ✅ Complete |

**Total: 22 / 22 phases completed.**

---

# 🧰 Technologies & Tools

## SIEM & Monitoring

- Wazuh
- Wazuh Manager
- Wazuh Agent
- Wazuh Dashboard
- Sysmon
- Windows Event Viewer
- PowerShell Operational Logging
- Windows Security Auditing

## Windows / Enterprise Infrastructure

- Windows Server
- Windows 11
- Active Directory Domain Services
- DNS
- Group Policy
- PowerShell
- Windows Security Logs

## Security Testing

- Kali Linux
- Nmap
- SMB enumeration
- Network connectivity testing
- Controlled discovery activity

## Detection & Investigation

- MITRE ATT&CK
- Wazuh rules
- Custom detection rules
- Event correlation
- Threat hunting
- Alert triage
- File hashing
- Authenticode validation
- False Positive analysis
- True Positive analysis

## Infrastructure & Documentation

- Oracle VirtualBox
- Git
- GitHub
- Visual Studio Code
- Markdown

---

# 📁 Repository Structure

```text
ENTERPRISE-SOC-LAB/
│
├── active-directory/
├── architecture/
├── assets/
├── attack-scenarios/
├── dashboards/
├── detection-rules/
├── diagrams/
├── docs/
│   ├── Phase-01/
│   ├── ...
│   ├── Phase-20/
│   └── Phase-22/
├── elastic/
├── incident-response/
├── infrastructure/
├── installation/
├── linux/
├── network/
├── reports/
├── screenshots/
│   ├── Phase-01/
│   ├── ...
│   ├── Phase-20/
│   └── Phase-22/
├── sigma/
├── SOC/
├── threat-hunting/
├── wazuh/
├── windows/
│
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
└── ROADMAP.md
```

Supporting documentation for some phases is organized in dedicated architecture, SOC, infrastructure, detection, and other repository directories rather than exclusively under `/docs`.

---

# 📸 Evidence & Documentation

Evidence collected throughout the project includes:

- VM configuration
- Network configuration
- Active Directory deployment
- Domain Controller configuration
- Organizational Units
- Security groups
- Group membership
- Security policies
- Windows domain membership
- Sysmon configuration
- Sysmon events
- PowerShell events
- Wazuh Agent status
- Wazuh telemetry
- Detection alerts
- MITRE ATT&CK mapping
- False Positive investigation
- True Positive investigation
- File hashes
- Digital signatures
- Threat-hunting results
- Incident timelines
- Post-investigation health validation

Screenshots are organized by project phase under:

```text
screenshots/
```

Phase-specific technical documentation is maintained throughout the repository.

---

# 🧠 Major Lessons Learned

## 1. Telemetry is not the same as an alert

An event can successfully reach a SIEM without generating an alert.

Understanding the difference between:

```text
Event Generation
Event Collection
Event Ingestion
Event Decoding
Rule Evaluation
Alert Generation
```

is critical when troubleshooting SIEM pipelines.

---

## 2. Alerts require investigation

A detection rule firing does not prove malicious activity.

Phase 20 demonstrated this directly when a T1046 detection was ultimately determined to be legitimate Wazuh Agent communication.

---

## 3. True Positives require evidence

A True Positive should only be declared when the analyst can prove that the detected activity actually occurred and matches the detection.

Phase 22 demonstrated this using:

```text
Get-Process
      ↓
PowerShell 4104
      ↓
Wazuh Rule 91815
      ↓
MITRE T1057
      ↓
TRUE POSITIVE
```

---

## 4. Legitimate tools can perform suspicious behavior

PowerShell is a legitimate administrative tool.

However, commands executed through PowerShell can represent attacker techniques.

Analysts must evaluate **behavior and context**, not simply whether a binary is legitimate.

---

## 5. Detection rules must be tuned

Broad detection logic can create False Positives.

Detection engineering requires:

```text
Create
   ↓
Test
   ↓
Investigate
   ↓
Tune
   ↓
Retest
```

---

## 6. Failed tests are still valuable

Not every attack simulation or experimental rule worked as originally intended.

Rather than fabricating successful results, failures and limitations were investigated and documented.

This reflects real SOC and detection-engineering work.

---

## 7. SIEM troubleshooting is part of SOC engineering

The project included configuration failures, decoder troubleshooting, service recovery, rule validation, telemetry verification, and post-change health checks.

Building detections is only part of operating a monitoring platform.

---

# 💼 Skills Demonstrated

This project demonstrates hands-on experience with:

### SOC Operations
- Security monitoring
- Alert triage
- Incident investigation
- False Positive analysis
- True Positive validation
- Threat hunting
- Incident documentation

### SIEM
- Wazuh deployment
- Wazuh Agent integration
- Log collection
- Rule analysis
- Custom detection testing
- SIEM troubleshooting
- Alert investigation

### Endpoint Security
- Windows Event Logs
- Sysmon
- PowerShell Script Block Logging
- Process investigation
- File hashing
- Digital signature validation

### Detection Engineering
- Detection-rule development
- Detection testing
- False Positive identification
- Rule tuning
- MITRE ATT&CK mapping
- Telemetry validation

### Enterprise Infrastructure
- Windows Server
- Active Directory
- DNS
- Organizational Units
- Security groups
- Group membership
- Domain-joined endpoints
- Security auditing

### Networking
- Enterprise network design
- TCP/IP
- Service discovery
- SMB
- Network telemetry
- Network connection investigation

### Security Testing
- Kali Linux
- Nmap
- Controlled attack simulation
- Discovery techniques

### Documentation & Engineering
- Git
- GitHub
- Visual Studio Code
- Markdown
- Technical documentation
- Evidence management

---

# 🎤 Interview Summary

## One-Line Explanation

> Built a 22-phase Enterprise SOC Lab using Active Directory, Windows 11, Sysmon, PowerShell logging and Wazuh SIEM to perform centralized security monitoring, detection engineering, MITRE ATT&CK mapping, controlled attack simulation, and both False Positive and True Positive incident investigations.

## Short Explanation

> I built an enterprise-style SOC lab from the infrastructure layer through incident investigation. I deployed Active Directory and a monitored Windows 11 endpoint, integrated Sysmon, Windows Security logs and PowerShell logging with Wazuh, generated controlled security activity, analyzed detections using MITRE ATT&CK, and investigated alerts. One T1046 alert was proven to be a False Positive caused by legitimate Wazuh Agent traffic, while a controlled PowerShell Process Discovery test generated Event ID 4104 and Wazuh Rule 91815 for T1057, which I investigated and classified as a True Positive.

## Detailed SOC Story

> The project taught me to follow the complete detection lifecycle rather than focusing only on generating SIEM alerts. I first built the enterprise infrastructure and Windows monitoring pipeline, then validated Windows Security, Sysmon and PowerShell telemetry centrally through Wazuh. During detection engineering, a broad T1046 rule generated alerts on legitimate Wazuh Agent network traffic. Instead of treating the alert as an attack, I investigated the process, destination port, endpoint service, file hash, digital signature and surrounding activity, and correctly closed the incident as a False Positive. I later performed controlled PowerShell Process Discovery using Get-Process. PowerShell Event ID 4104 captured the exact command, Wazuh Rule 91815 detected the behavior and mapped it to MITRE ATT&CK T1057, and I correlated the endpoint and SIEM evidence before classifying it as a True Positive. This gave the project examples of both major alert-classification outcomes and demonstrated practical SOC investigation rather than only SIEM installation.

---

# 🔐 Ethical Use

All security testing performed as part of this project was conducted in a controlled laboratory environment.

The techniques and tools demonstrated in this repository are intended for:

- Cybersecurity education
- Defensive security research
- SOC training
- Detection engineering
- Authorized security testing

They should only be used on systems where explicit authorization has been provided.

---

# 🚀 Final Project Result

The **Enterprise SOC Lab is complete through Phase 22**.

The final environment demonstrates the complete SOC lifecycle:

```text
Enterprise Infrastructure
          ↓
Endpoint Monitoring
          ↓
Centralized SIEM
          ↓
Detection Engineering
          ↓
Controlled Security Testing
          ↓
MITRE ATT&CK Mapping
          ↓
Alert Triage
          ↓
Investigation
          ↓
False Positive / True Positive Classification
          ↓
Response Decision
          ↓
Post-Investigation Validation
          ↓
Documentation
```

The project progressed from building basic enterprise infrastructure to performing evidence-based SOC investigations.

Most importantly, the project demonstrates that effective security operations are not about treating every alert as an attack.

They are about collecting reliable telemetry, understanding detections, investigating evidence, determining context, making defensible decisions, and documenting the results.

---

# 👤 Author

**Faraz Shaikh**

Cybersecurity | SOC Operations | Detection Engineering | Penetration Testing | Digital Forensics

GitHub: `farazshk152-Cybersecurity-Portfolio`

---

## Project Completion

```text
ENTERPRISE SOC LAB
22 / 22 PHASES COMPLETE
STATUS: COMPLETE
```

**Final Phase:** Phase 22 — True Positive Detection & Incident Investigation

**Final TP Case:** T1057 — Process Discovery — TRUE POSITIVE

**Final FP Case:** T1046 — Network Service Discovery — FALSE POSITIVE