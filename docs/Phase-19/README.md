# Phase 19 – Attack Simulation & Detection Engineering

## Objective

Phase 19 focused on generating controlled Windows attack-like telemetry, validating Sysmon network events in Wazuh, developing a MITRE ATT&CK T1046 detection, investigating false positives, and safely tuning the detection logic.

The objective was not simply to generate alerts, but to demonstrate a realistic detection-engineering workflow:

Attack Simulation → Endpoint Telemetry → SIEM Ingestion → Detection → Investigation → False-Positive Analysis → Rule Tuning → Validation → Cleanup

---

## Environment

### Wazuh Manager
- Host: Wazuh Server
- IP: 192.168.10.30
- Platform: Wazuh 4.14.7

### Windows Endpoint
- Hostname: WIN11-CLIENT01
- IP: 192.168.10.20
- Wazuh Agent ID: 002
- Sysmon enabled
- Microsoft-Windows-Sysmon/Operational monitored by Wazuh

---

## MITRE ATT&CK Technique

### T1046 – Network Service Discovery

Network connection activity was generated from WIN11-CLIENT01 using controlled PowerShell network tests.

Example:

Test-NetConnection 192.168.10.30 -Port 55000 -InformationLevel Quiet

The activity generated Sysmon Event ID 3 network connection telemetry.

---

## Sysmon Telemetry Validation

Sysmon Event ID 3 events were successfully generated on WIN11-CLIENT01.

Observed telemetry included:

- Provider: Microsoft-Windows-Sysmon
- Event ID: 3
- Image: powershell.exe
- Source IP: 192.168.10.20
- Destination IP: 192.168.10.30
- Destination Port: 55000
- Protocol: TCP
- Initiated: true

The events were successfully forwarded by the Wazuh Agent and observed on the Wazuh Manager.

This validated the telemetry pipeline:

PowerShell
→ Sysmon
→ Windows Event Channel
→ Wazuh Agent
→ Wazuh Manager
→ Wazuh Archives / Dashboard

---

## Initial T1046 Detection

A custom Phase 19 detection rule was created to identify Sysmon network connection activity and map it to MITRE ATT&CK T1046.

The initial rule successfully generated Level 8 T1046 alerts.

Wazuh Dashboard verification confirmed T1046 alerts associated with WIN11-CLIENT01.

---

## False-Positive Investigation

Investigation of the generated T1046 alerts showed that the initial detection was too broad.

The rule matched legitimate Wazuh Agent network communication.

Observed process:

C:\Program Files (x86)\ossec-agent\wazuh-agent.exe

Observed Wazuh communication included destination ports such as:

- 1514
- 1515

Therefore, although the detection successfully generated T1046 alerts, it also classified legitimate Wazuh infrastructure communication as network service discovery.

This represented a detection false positive.

---

## Detection Tuning

A narrower experimental rule (Rule ID 100101) was developed to restrict detection to PowerShell-generated Sysmon Event ID 3 network activity.

The tuning process investigated:

- Sysmon Event ID 3
- Parent Sysmon rule 61605
- PowerShell image matching
- initiated=true
- destination port filtering
- windows_eventchannel decoding
- MITRE T1046 mapping

Multiple rule iterations were validated using:

/var/ossec/bin/wazuh-analysisd -t

The final PowerShell-specific experimental rule passed Wazuh configuration validation.

However, live PowerShell Sysmon Event ID 3 telemetry continued to reach archives.json without reliably producing Rule 100101 alerts.

The detection was therefore not falsely documented as successful.

Instead, the experimental rule was disabled and preserved for future tuning:

phase19_t1046_rules.xml.disabled

This prevented unreliable detection logic from remaining active in the SIEM.

---

## Detection Engineering Outcome

Phase 19 demonstrated both successful detection and detection tuning.

### Verified

- Controlled PowerShell network activity generated
- Sysmon Event ID 3 generated
- Windows Sysmon telemetry collected by Wazuh
- Event ID 3 observed in Wazuh archives
- Source and destination network information captured
- Initial custom T1046 rule generated alerts
- MITRE ATT&CK T1046 visible in Wazuh Dashboard
- False-positive traffic identified
- Legitimate wazuh-agent.exe communication investigated
- PowerShell-specific detection tuning attempted
- Experimental rule configuration validated
- Unreliable experimental detection safely disabled
- Wazuh Manager returned to a healthy state

### Detection Engineering Lesson

A SIEM alert firing successfully does not automatically mean that the detection is high quality.

The initial T1046 detection produced alerts but also matched legitimate Wazuh Agent traffic. Investigation and tuning were therefore necessary.

The Phase 19 workflow demonstrated:

Detection → Validation → Investigation → False-Positive Identification → Tuning → Safe Rollback

This reflects a realistic SOC detection-engineering process.

---

## Cleanup

Temporary archive logging used during troubleshooting was disabled after validation.

Final configuration:

<logall>no</logall>
<logall_json>no</logall_json>

Temporary Rule 100002 was confirmed absent.

The experimental PowerShell-specific T1046 rule was preserved as:

phase19_t1046_rules.xml.disabled

Wazuh configuration validation completed successfully and the Wazuh Manager remained active.

---

## Dashboard Validation

Wazuh Discover was queried using:

agent.name:"WIN11-CLIENT01"

The dashboard returned active Windows endpoint telemetry.

A MITRE-specific query was also performed:

agent.name:"WIN11-CLIENT01" AND rule.mitre.id:"T1046"

Two T1046 hits were observed.

Investigation showed that these alerts corresponded to the earlier broad detection and included legitimate wazuh-agent.exe network communication, confirming the false-positive condition.

---

## Evidence

Phase 19 evidence was captured under:

screenshots/Phase-19/

Key final evidence includes:

### Screenshot 12
12-Phase19-T1046-Dashboard-False-Positive-Evidence.png

Demonstrates:
- WIN11-CLIENT01
- MITRE T1046 query
- Two T1046 alerts
- Wazuh Agent network traffic
- False-positive investigation evidence

### Screenshot 13
13-Phase19-Final-Validation-Cleanup.png

Demonstrates:
- Wazuh Manager healthy
- logall disabled
- logall_json disabled
- Experimental T1046 rule safely disabled
- Agent connectivity / final Phase 19 state

---

## Phase 19 Status

**COMPLETED**

Phase 19 successfully demonstrated controlled attack simulation, Sysmon telemetry generation, Wazuh ingestion, MITRE ATT&CK detection engineering, false-positive investigation, rule tuning, safe rollback, SIEM validation, and configuration cleanup.

The environment is healthy and ready for Phase 20.