## Phase 22 — True Positive Detection & Incident Investigation

### Added
- Added a controlled True Positive detection and SOC investigation.
- Executed controlled PowerShell Process Discovery on WIN11-CLIENT01.
- Used `Get-Process | Select-Object -First 10` as the controlled discovery activity.
- Verified PowerShell Script Block Logging captured the exact command.
- Verified Windows PowerShell Operational Event ID 4104.
- Correlated the endpoint activity with Wazuh Agent 002.
- Verified Wazuh Rule 91815 generated a Process Discovery detection.
- Verified MITRE ATT&CK mapping to T1057 — Process Discovery.
- Investigated the PowerShell executable used during analysis.
- Collected the SHA-256 hash of `powershell.exe`.
- Verified the PowerShell executable had a valid Authenticode signature.
- Independently validated WIN11-CLIENT01 hostname and 192.168.10.20 endpoint address.
- Performed post-investigation Wazuh Agent health validation.
- Added Phase 22 documentation and evidence screenshots.

### Investigation Findings
- Endpoint: `WIN11-CLIENT01`
- Endpoint IP: `192.168.10.20`
- Wazuh Agent ID: `002`
- Controlled command: `Get-Process | Select-Object -First 10`
- Windows Event ID: `4104`
- Wazuh Rule ID: `91815`
- Wazuh Rule Level: `4`
- Detection: `Powershell executing process discovery`
- MITRE ATT&CK: `T1057 — Process Discovery`
- Tactic: `Discovery`
- PowerShell path: `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe`
- SHA-256: `7600FFE12DA441FE89D035B13801E8E91D064BC544A27B19A5CF49F6AB8B18F5`
- Authenticode status: `Valid`
- User attribution: Not available in the captured Event ID 4104 alert.

### Classification
**TRUE POSITIVE — Authorized Controlled Security Test**

The alert was classified as a True Positive because the Process Discovery activity actually occurred, the exact command was captured through PowerShell Event ID 4104, and Wazuh Rule 91815 correctly detected and mapped the activity to MITRE ATT&CK T1057.

No containment, credential reset, process termination, host isolation, or escalation was required because the activity was an authorized laboratory simulation.

### Post-Investigation Validation
- Wazuh Agent 002 remained Active.
- WIN11-CLIENT01 monitoring remained operational.
- No production-style containment action was required.
- Existing stale Agent 001 was left unchanged.

### Project Outcome
The Enterprise SOC Lab now demonstrates both alert-classification outcomes:

- Phase 20: T1046 — **FALSE POSITIVE**
- Phase 22: T1057 — **TRUE POSITIVE**

**Phase 22 Status: COMPLETE**

---

## Final Project Status

**Enterprise SOC Lab: COMPLETE**

**22 / 22 phases completed.**

The completed project demonstrates enterprise infrastructure, Active Directory, endpoint telemetry, Sysmon, PowerShell monitoring, Wazuh SIEM, detection engineering, MITRE ATT&CK mapping, controlled security testing, False Positive investigation, True Positive investigation, incident response, threat hunting, evidence collection, and SOC documentation.