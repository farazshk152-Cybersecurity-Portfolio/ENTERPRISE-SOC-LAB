# Enterprise SOC Lab - Changelog

This changelog records the major implementation, security monitoring, detection engineering, and investigation milestones completed throughout the Enterprise SOC Lab.

---

## Phase 01 - Project Planning & Repository Initialization

- Established the Enterprise SOC Lab project.
- Created the initial repository structure.
- Defined project objectives and documentation strategy.
- Prepared the environment for structured phase-based implementation.

## Phase 02 - Infrastructure Planning

- Planned the virtual enterprise infrastructure.
- Defined system roles and network requirements.
- Prepared the architecture for Windows, Linux, SIEM, and attacker systems.

## Phase 03 - Virtualization Platform Setup

- Configured VirtualBox as the virtualization platform.
- Prepared isolated networking for the enterprise lab.
- Established the foundation for virtual machine deployment.

## Phase 04 - Windows Server Deployment

- Deployed the Windows Server environment.
- Performed initial server configuration.
- Prepared the server for enterprise identity services.

## Phase 05 - Active Directory Deployment

- Installed and configured Active Directory components.
- Prepared centralized authentication and domain services.

## Phase 06 - Enterprise Environment Overview

- Documented the enterprise lab structure.
- Defined system roles and security-monitoring objectives.

## Phase 07 - Active Directory Architecture & Implementation

Designed the Active Directory architecture and documented:

- Forest design
- OU structure
- User strategy
- Security groups
- Service accounts
- Administrative accounts
- Computer objects
- Group Policy strategy

## Phase 08 - Enterprise Network Architecture

Designed and documented the enterprise network architecture, including:

- Network overview
- IP addressing
- Network segmentation
- DNS design
- DHCP considerations
- Firewall strategy
- Remote access considerations
- Network security

## Phase 09 - Security Operations Center Design

Designed the Security Operations Center and documented:

- SOC overview
- Asset classification
- Log sources
- Monitoring strategy
- Alert priorities
- Detection use cases
- SOC workflow
- Key metrics

## Phase 10 - Detection Engineering

- Developed the detection-engineering component of the lab.
- Defined security monitoring and detection concepts for later SIEM implementation.
- Prepared the project for telemetry-driven detection development.

## Phase 11 - Windows Server Rebuild & Domain Controller Promotion

- Rebuilt the Windows Server environment where required.
- Promoted the server to the Domain Controller role.
- Restored the Active Directory foundation required for later enterprise phases.

## Phase 12 - Organizational Unit Design

- Implemented the planned Organizational Unit structure.
- Organized Active Directory objects according to the enterprise design.

## Phase 13 - Security Groups

- Created security groups required by the enterprise Active Directory design.
- Prepared group-based access and administrative organization.

## Phase 14 - Active Directory Group Membership

- Configured Active Directory group membership.
- Validated relationships between users and security groups.

## Phase 15 - Security Policies & Auditing

- Configured Windows security and auditing policies.
- Improved visibility into security-relevant Windows activity.
- Prepared the environment for centralized security monitoring.

## Phase 16 - Windows 11 Domain Join

- Integrated the Windows 11 workstation with the enterprise domain.
- Validated domain connectivity and endpoint integration.
- Prepared WIN11-CLIENT01 for centralized monitoring.

## Phase 17 - Kali Linux Attacker Setup

- Configured Kali Linux as the controlled attacker system.
- Validated enterprise network connectivity.
- Performed controlled service and SMB enumeration testing.
- Generated Sysmon network, file creation, and DNS telemetry.
- Documented unsuccessful/blocked tests where services were unavailable rather than fabricating successful results.

## Phase 18 - Wazuh SIEM Deployment & Log Collection

- Integrated WIN11-CLIENT01 with Wazuh.
- Configured centralized Windows security telemetry collection.
- Enabled collection of Sysmon Operational events.
- Enabled collection of PowerShell Operational events.
- Verified Windows Security Event ID 4688 telemetry.
- Verified PowerShell Event ID 4104 telemetry.
- Verified central ingestion of Sysmon telemetry.
- Investigated native Wazuh Sysmon rule behavior.
- Confirmed that Sysmon Event ID 11 could reach central archives even when the corresponding native rule operated at level 0.
- Resolved a malformed custom decoder configuration without modifying native Wazuh rules.
- Restored healthy Wazuh Manager operation and endpoint connectivity.
- Returned temporary archive logging settings to their normal disabled state.

## Phase 19 - Attack Simulation & Detection Engineering

- Performed controlled T1046 Network Service Discovery detection testing.
- Generated Sysmon Event ID 3 network telemetry from WIN11-CLIENT01.
- Verified telemetry arrival at the Wazuh Manager.
- Investigated the native Wazuh Sysmon rule chain.
- Developed custom Wazuh detection rule 100100.
- Generated MITRE ATT&CK T1046 alerts.
- Identified false positives involving legitimate `wazuh-agent.exe` communication.
- Investigated and attempted narrower detection logic.
- Preserved the unsuccessful experimental rule in a disabled state.
- Documented detection limitations instead of claiming an unverified successful result.
- Restored normal Wazuh logging configuration after testing.

## Phase 20 - Incident Response & SOC Investigation

Investigated the Phase 19 T1046 alert using a structured SOC workflow.

The investigated alert included:

- Endpoint: WIN11-CLIENT01
- Endpoint IP: 192.168.10.20
- Process: `wazuh-agent.exe`
- PID: 2240
- Destination: 192.168.10.30:1514/TCP
- Wazuh Rule ID: 100100
- MITRE ATT&CK: T1046 - Network Service Discovery
- Severity Level: 8

Investigation activities included:

- Initial alert triage
- Endpoint identification
- User and process validation
- Network indicator analysis
- Wazuh Manager port validation
- Wazuh Agent status validation
- Process ID correlation
- SHA256 hashing
- Authenticode signature validation
- Threat hunting for related activity
- Incident timeline reconstruction
- MITRE ATT&CK mapping
- False-positive analysis
- Post-investigation health validation

SHA256 examined:

`7C98FE80900087FF12CC629842ED9D62754AFF65E81CF7790BA09984B7A64B4D`

The investigation determined that the alert represented legitimate Wazuh Agent communication with the Wazuh Manager.

Final classification:

**FALSE POSITIVE**

Final status:

**CLOSED - FALSE POSITIVE**

Root cause:

The Phase 19 custom detection rule was overly broad and classified expected Wazuh Agent network communication as T1046 activity.

Recommended action:

Tune or disable overly broad detection logic while retaining visibility into genuinely suspicious network discovery behavior.

---

## Phase 21 - Final Documentation, Validation & Release

In progress.

Completed so far:

- Audited repository structure.
- Audited Phase 01-20 documentation coverage.
- Audited screenshot directories for Phase 01-20.
- Removed an accidental empty architecture file.
- Reconstructed the missing Phase 20 README.
- Corrected outdated WAZUH01 operating-system references to Amazon Linux 2023.
- Created the main project README.
- Updated the project ROADMAP.
- Expanded the project CHANGELOG.

Remaining:

- Final repository cleanup and validation.
- Git status review.
- Logical final commits.
- Push to main.
- GitHub verification.
- Final portfolio review.