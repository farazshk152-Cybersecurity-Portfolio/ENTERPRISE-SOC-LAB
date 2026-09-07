# Enterprise SOC Lab — Project Roadmap

## Project Status

**COMPLETE ✅**

**22 / 22 Phases Completed**

The Enterprise SOC Lab has progressed from initial infrastructure planning through enterprise deployment, centralized security monitoring, detection engineering, controlled attack simulation, False Positive investigation, True Positive investigation, and final SOC documentation.

---

# Project Roadmap

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

---

# Major Milestones

## Enterprise Infrastructure

- [x] Project repository created
- [x] VirtualBox environment configured
- [x] Enterprise network designed
- [x] Windows Server deployed
- [x] Active Directory deployed
- [x] Domain Controller configured
- [x] Organizational Units created
- [x] Security groups configured
- [x] Group memberships configured
- [x] Security policies and auditing configured
- [x] Windows 11 endpoint joined to enterprise environment

---

## Endpoint Monitoring

- [x] Windows Security auditing validated
- [x] Sysmon deployed
- [x] Sysmon network telemetry validated
- [x] Sysmon file creation telemetry validated
- [x] Sysmon DNS telemetry validated
- [x] PowerShell Operational Logging validated
- [x] PowerShell Script Block Logging validated
- [x] PowerShell Event ID 4104 captured

---

## SIEM Integration

- [x] Wazuh Manager deployed
- [x] Wazuh Agent installed
- [x] WIN11-CLIENT01 registered as Agent 002
- [x] Windows Security logs collected
- [x] Sysmon logs collected
- [x] PowerShell logs collected
- [x] Centralized telemetry validated
- [x] Wazuh configuration troubleshooting completed
- [x] Wazuh Manager health validated
- [x] Agent 002 connectivity validated

---

## Detection Engineering

- [x] Controlled security activity generated
- [x] Sysmon telemetry analyzed
- [x] Wazuh native rule behavior investigated
- [x] Custom detection rule tested
- [x] MITRE ATT&CK mapping implemented
- [x] T1046 detection investigated
- [x] False Positive identified
- [x] Detection tuning limitations documented
- [x] Experimental detection safely disabled where appropriate

---

## Incident Response

- [x] Alert triage performed
- [x] Endpoint identified
- [x] Process investigated
- [x] Network indicators analyzed
- [x] File hash collected
- [x] Digital signature validated
- [x] MITRE ATT&CK technique analyzed
- [x] Threat hunt performed
- [x] Incident timeline developed
- [x] Severity assessed
- [x] Containment decision documented
- [x] Recovery/health validation performed
- [x] False Positive case closed

---

# Phase 20 Milestone — False Positive Investigation

Detection:

**T1046 — Network Service Discovery**

Wazuh Rule:

**100100**

Observed process:

`wazuh-agent.exe`

Investigation determined that the detected network communication was legitimate Wazuh Agent traffic to the Wazuh Manager.

Final classification:

**FALSE POSITIVE**

Incident status:

**CLOSED — FALSE POSITIVE**

This demonstrated evidence-based SOC alert triage and detection tuning.

---

# Phase 21 Milestone — Repository Finalization

- [x] Phase documentation reviewed
- [x] Root README expanded
- [x] ROADMAP updated
- [x] CHANGELOG expanded
- [x] Repository structure audited
- [x] Accidental temporary files removed
- [x] Empty diagram placeholders removed
- [x] Architecture OS references corrected
- [x] CONTRIBUTING documentation added
- [x] MIT LICENSE added
- [x] Git working tree validated
- [x] Changes committed
- [x] Main branch pushed to GitHub

Phase 21 established a clean and documented release state before the project was extended with Phase 22.

---

# Phase 22 Milestone — True Positive Investigation

Controlled activity:

`Get-Process | Select-Object -First 10`

Endpoint:

**WIN11-CLIENT01**

Endpoint IP:

**192.168.10.20**

Wazuh Agent:

**002**

Windows telemetry:

**PowerShell Event ID 4104**

Wazuh detection:

**Rule 91815 — Powershell executing process discovery**

MITRE ATT&CK:

**T1057 — Process Discovery**

Tactic:

**Discovery**

The exact controlled PowerShell command was captured by Script Block Logging and correlated with the Wazuh detection.

Final classification:

**TRUE POSITIVE**

Context:

**Authorized Controlled Security Test**

Post-investigation validation confirmed that Agent 002 remained Active.

---

# Final Detection Outcomes

The completed Enterprise SOC Lab contains both major SOC alert-classification outcomes:

| Case | MITRE Technique | Classification |
|---|---|---|
| Phase 20 | T1046 — Network Service Discovery | FALSE POSITIVE |
| Phase 22 | T1057 — Process Discovery | TRUE POSITIVE |

This demonstrates that alerts were investigated and classified based on evidence rather than automatically treated as malicious activity.

---

# Final Capabilities Demonstrated

The completed project demonstrates hands-on experience with:

- Enterprise infrastructure
- Active Directory
- Windows security monitoring
- Sysmon
- PowerShell logging
- Wazuh SIEM
- Centralized log collection
- Detection engineering
- Custom rule testing
- MITRE ATT&CK
- Controlled attack simulation
- Alert triage
- Threat hunting
- False Positive analysis
- True Positive analysis
- Incident response
- File hashing
- Digital signature verification
- Detection tuning
- SIEM troubleshooting
- Evidence collection
- Technical documentation
- Git and GitHub

---

# Final Status

```text
ENTERPRISE SOC LAB

PHASES COMPLETED: 22 / 22
PROJECT STATUS: COMPLETE

FALSE POSITIVE CASE:
T1046 — Network Service Discovery

TRUE POSITIVE CASE:
T1057 — Process Discovery