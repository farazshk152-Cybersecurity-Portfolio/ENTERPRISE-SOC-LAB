# Phase 18 — Wazuh SIEM Deployment & Log Collection

## Objective

Phase 18 validates the Wazuh SIEM pipeline from the Windows 11 endpoint through the Wazuh Agent and Manager to centralized event storage and Dashboard visibility.

The phase covers:

- Wazuh Manager health
- Wazuh Agent connectivity
- Sysmon telemetry
- Windows Security telemetry
- PowerShell telemetry
- Wazuh EventChannel collection
- Centralized Sysmon Event ID 11 ingestion
- Wazuh rule and alert validation
- Dashboard access
- Configuration validation and cleanup

---

## Lab Architecture

| Component | Address / Identifier |
|---|---|
| Domain | `enterprise.local` |
| DC01 | `192.168.10.10` |
| WIN11-CLIENT01 | `192.168.10.20` |
| Wazuh Server | `192.168.10.30` |
| Wazuh Agent | Agent 002 |
| Wazuh Version | `4.14.7` |
| Sysmon | `15.21` |
| Wazuh Server OS | Amazon Linux 2023 |

WIN11-CLIENT01 uses the enterprise network `192.168.10.0/24` and the Wazuh server is reachable at `192.168.10.30`.

---

## Wazuh Manager

The Wazuh Manager was repaired after a malformed custom Sysmon decoder caused an analysis configuration failure.

The malformed decoder was preserved as a backup and removed from the active decoder path.

The Wazuh analysis configuration was subsequently validated successfully using:

```bash
sudo /var/ossec/bin/wazuh-analysisd -t