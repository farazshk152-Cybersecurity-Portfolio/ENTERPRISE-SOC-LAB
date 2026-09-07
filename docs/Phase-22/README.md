# Phase 22 — True Positive Detection & Incident Investigation

## Overview

Phase 22 extends the Enterprise SOC Lab by demonstrating a verified True Positive security detection and SOC investigation.

Earlier phases established Windows telemetry collection, Wazuh SIEM integration, detection engineering, MITRE ATT&CK mapping, and False Positive investigation.

During Phase 20, a T1046 Network Service Discovery alert was investigated and determined to be a False Positive caused by legitimate Wazuh Agent communication.

Phase 22 demonstrates the opposite outcome: an intentionally executed, controlled Process Discovery activity was successfully captured by Windows PowerShell logging, forwarded to Wazuh, detected by an existing Wazuh rule, mapped to MITRE ATT&CK, investigated, and correctly classified as a True Positive.

All activity was performed inside the isolated Enterprise SOC Lab.

---

# TP-01 — PowerShell Process Discovery

## Objective

The objective of TP-01 was to generate controlled Process Discovery activity on WIN11-CLIENT01 and verify the complete detection lifecycle:

1. Execute controlled discovery activity.
2. Capture endpoint telemetry.
3. Verify the exact activity in Windows logs.
4. Verify Wazuh detection.
5. Identify the affected endpoint.
6. Map the behavior to MITRE ATT&CK.
7. Investigate the executable involved.
8. Determine whether the alert represents a True Positive or False Positive.
9. Perform post-investigation health validation.

---

## Environment

| Component | Value |
|---|---|
| Endpoint | WIN11-CLIENT01 |
| Endpoint IP | 192.168.10.20 |
| Wazuh Agent ID | 002 |
| SIEM | Wazuh |
| PowerShell Log | Microsoft-Windows-PowerShell/Operational |
| PowerShell Event ID | 4104 |
| Wazuh Rule ID | 91815 |
| Wazuh Rule Level | 4 |
| MITRE ATT&CK ID | T1057 |
| MITRE Technique | Process Discovery |
| MITRE Tactic | Discovery |

---

## 1. Controlled Activity

The following read-only PowerShell command was intentionally executed on WIN11-CLIENT01:

```powershell
Get-Process | Select-Object -First 10