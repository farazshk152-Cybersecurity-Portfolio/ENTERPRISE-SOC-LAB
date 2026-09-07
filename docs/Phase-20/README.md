# Phase 20 - Incident Response & SOC Investigation

## Objective

Investigate a Wazuh alert generated during Phase 19 detection engineering, perform SOC analyst triage, validate endpoint and network activity, determine whether the alert represents malicious activity or a false positive, and document the incident response process.

---

## Incident Summary

A Wazuh alert was generated for MITRE ATT&CK technique:

- Technique: Network Service Discovery
- MITRE ID: T1046
- Tactic: Discovery
- Wazuh Rule ID: 100100
- Severity Level: 8
- Endpoint: WIN11-CLIENT01
- Endpoint IP: 192.168.10.20
- Wazuh Manager: 192.168.10.30

The investigation focused on determining whether the detected network connection represented real network service discovery or legitimate Wazuh Agent communication.

Final disposition:

**CLOSED - FALSE POSITIVE**

---

## Initial Alert Triage

The Wazuh Dashboard was searched using:

`agent.name:"WIN11-CLIENT01" AND rule.mitre.id:"T1046"`

Two alerts were identified within the selected time range.

The primary investigated alert showed:

- Agent ID: 002
- Agent Name: WIN11-CLIENT01
- Agent IP: 192.168.10.20
- Manager: wazuh-server
- Rule ID: 100100
- Rule Level: 8
- MITRE ID: T1046
- MITRE Technique: Network Service Discovery
- Tactic: Discovery
- Decoder: windows_eventchannel
- Event Channel: Microsoft-Windows-Sysmon/Operational
- Sysmon Event ID: 3

Selected Dashboard timestamp:

- Sep 5, 2026 @ 17:36:03.564

Second related alert:

- Sep 5, 2026 @ 14:13:21.620

The event also contained:

- Process: `C:\Program Files (x86)\ossec-agent\wazuh-agent.exe`
- Process ID: 2240
- User: `NT AUTHORITY\SYSTEM`
- Protocol: TCP
- Source IP: 192.168.10.20
- Source Port: 55410
- Destination IP: 192.168.10.30
- Destination Port: 1514
- Initiated: true
- Process GUID: `{4bf57be3-18b4-6a98-3700-000000001900}`

The event data also contained:

- `eventdata.utcTime: 2026-09-02 16:16:46.264`

The Dashboard timestamp was used as the primary investigation timeline reference.

---

## Network Investigation

The destination IP was the Wazuh Manager:

`192.168.10.30`

The destination port was:

`1514/TCP`

The Wazuh Manager was checked to confirm whether this port was legitimately used by the Wazuh infrastructure.

Command used:

`sudo ss -lntp | grep 1514`

The result confirmed that Wazuh `remoted` was listening on TCP port 1514.

Agent status was also validated using:

`sudo /var/ossec/bin/agent_control -l`

The result confirmed:

- Agent ID 002
- WIN11-CLIENT01
- Status: Active

This established that the destination IP and port were consistent with normal Wazuh Agent-to-Manager communication.

---

## Endpoint Process Investigation

The Wazuh Agent service was checked on WIN11-CLIENT01.

The service:

`WazuhSvc`

was confirmed to be running.

The related process was also validated:

`wazuh-agent.exe`

The process was running with:

- PID: 2240
- Expected Wazuh installation path

The PID exactly matched the PID recorded in the Wazuh alert.

This strongly correlated the network event with the legitimate Wazuh Agent process.

---

## File Integrity Investigation

The executable investigated was:

`C:\Program Files (x86)\ossec-agent\wazuh-agent.exe`

Observed properties:

- File Length: 1217344 bytes
- Creation Time: 10-07-2026 09:20:28
- Authenticode Signature Status: Valid

SHA256:

`7C98FE80900087FF12CC629842ED9D62754AFF65E81CF7790BA09984B7A64B4D`

The valid signature was treated as supporting evidence together with the expected path, running service, process identity, PID correlation, and legitimate network destination.

---

## Threat Hunting

A follow-up search was performed to identify similar Wazuh Agent network activity from WIN11-CLIENT01.

Query:

`agent.name:"WIN11-CLIENT01" AND data.win.eventdata.image:*wazuh-agent.exe*`

The search returned two relevant events.

Both were associated with legitimate Wazuh Agent communication to:

`192.168.10.30:1514/TCP`

No unexpected external destination or evidence of actual network service discovery was identified during the investigation.

---

## Incident Timeline

### Event 1

- Sep 5, 2026 @ 14:13:21.620
- T1046 alert observed
- Process identified as `wazuh-agent.exe`
- Destination associated with the Wazuh Manager

### Event 2

- Sep 5, 2026 @ 17:36:03.564
- Second T1046 alert observed
- Same legitimate Wazuh Agent communication pattern

### Investigation

The SOC investigation validated:

- Wazuh Manager listening on port 1514
- Agent ID 002 active
- WazuhSvc running
- wazuh-agent.exe running from the expected path
- Alert PID matching the legitimate process PID
- Valid Authenticode signature
- Consistent SHA256 evidence
- No unexpected network destination
- No additional suspicious discovery activity

---

## Indicators Investigated

| Indicator | Value |
|---|---|
| Endpoint | WIN11-CLIENT01 |
| Endpoint IP | 192.168.10.20 |
| Destination IP | 192.168.10.30 |
| Destination Port | 1514/TCP |
| Process | wazuh-agent.exe |
| Process ID | 2240 |
| User | NT AUTHORITY\SYSTEM |
| Sysmon Event ID | 3 |
| Rule ID | 100100 |
| MITRE Technique | T1046 - Network Service Discovery |
| SHA256 | 7C98FE80900087FF12CC629842ED9D62754AFF65E81CF7790BA09984B7A64B4D |

---

## SOC Analyst Disposition

Classification:

**False Positive**

Analyst Assessment:

**Benign / Expected Activity**

Root Cause:

The Phase 19 custom detection rule was too broad and interpreted legitimate Wazuh Agent network communication as T1046 Network Service Discovery activity.

No evidence was identified indicating that WIN11-CLIENT01 was performing malicious network discovery.

---

## Incident Response Decision

Because the activity was validated as legitimate Wazuh infrastructure communication:

- Host isolation was not required.
- Process termination was not required.
- Credential reset was not required.
- Containment was not required.
- Eradication was not required.
- Escalation was not required.

The appropriate response was to tune or disable the overly broad detection logic rather than disrupt the endpoint.

---

## Recommended Remediation

The Phase 19 detection rule should exclude known legitimate Wazuh Agent communication while preserving visibility into suspicious network discovery behavior.

Known legitimate communication identified during this investigation:

`WIN11-CLIENT01 -> WAZUH01:1514/TCP`

The investigation demonstrates the importance of validating custom detection logic against expected infrastructure traffic before promoting a rule into production monitoring.

---

## Post-Investigation Validation

After completing the investigation:

- Wazuh Manager remained healthy.
- Agent ID 002 remained active.
- WIN11-CLIENT01 remained connected.
- No endpoint containment was required.
- No production-like lab service was intentionally disrupted.

---

## Evidence

The investigation was documented using the following screenshots:

1. `01-Phase20-Initial-T1046-Alert-Triage.png`
2. `02-Phase20-Wazuh-Port1514-Agent-Validation.png`
3. `03-Phase20-Wazuh-Agent-Process-Validation.png`
4. `04-Phase20-Process-Hash-Signature-Validation.png`
5. `05-Phase20-Threat-Hunt-Wazuh-Agent-Network-Activity.png`
6. `06-Phase20-Incident-Timeline-T1046.png`
7. `07-Phase20-Post-Investigation-Health-Validation.png`

Evidence directory:

`../../screenshots/Phase-20/`

---

## Key SOC Lessons

This phase demonstrated several core SOC investigation concepts:

- An alert is not automatically an incident.
- Detection rules must be validated against legitimate infrastructure behavior.
- Process identity should be correlated with service state, file path, PID, network destination, and file signature.
- Threat hunting should be used to determine whether an alert is isolated or part of a broader pattern.
- False positives should be documented and used to improve detection engineering.
- Containment should only be performed when evidence justifies the action.

---

## Outcome

The T1046 alert was fully investigated and determined to be legitimate Wazuh Agent communication.

The investigation successfully demonstrated:

- Alert triage
- Endpoint validation
- Process investigation
- Network investigation
- File hash and signature validation
- Threat hunting
- MITRE ATT&CK mapping
- False-positive classification
- Incident response decision-making
- Post-investigation health validation

Final Status:

**CLOSED - FALSE POSITIVE**

Phase 20 is complete.