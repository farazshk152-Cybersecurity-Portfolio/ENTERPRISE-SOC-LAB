# Phase 10 - Detection Engineering

## Objective

Develop the first detection use case for the Enterprise SOC Lab and document how security events will be identified, investigated, and mapped to MITRE ATT&CK.

The initial detection focuses on repeated failed Windows authentication attempts that may indicate password guessing or brute-force activity.

---

## Detection Use Case

### Brute Force Detection

The detection identifies repeated failed authentication attempts against Windows and Active Directory accounts.

The use case considers:

- Multiple failed logon attempts from the same source
- Multiple accounts being targeted
- A successful logon occurring after repeated failures
- The source system and affected account
- Whether the activity is expected or suspicious

---

## MITRE ATT&CK Mapping

**Technique:** T1110 - Brute Force

The detection is intended to identify authentication activity consistent with password guessing or brute-force behavior.

---

## Windows Event IDs

| Event ID | Description |
|---|---|
| 4625 | Failed logon |
| 4624 | Successful logon |

Event 4625 is the primary event used to identify failed authentication attempts.

Event 4624 can be reviewed to determine whether successful authentication occurred after repeated failures.

---

## Data Sources

The detection can use the following sources:

- Windows Security Logs
- Active Directory authentication events
- Sysmon events when available

---

## Detection Logic

An alert should be considered when repeated authentication failures are observed.

Example investigation conditions:

1. Multiple Event ID 4625 records occur.
2. The events originate from the same source.
3. One or more usernames are repeatedly targeted.
4. A successful Event ID 4624 occurs after the failures.
5. The activity is investigated to determine whether it is legitimate or malicious.

---

## Severity

**High**

Repeated authentication failures can indicate credential attacks and should be investigated when the activity exceeds normal user behavior.

---

## Investigation Procedure

1. Identify the source IP address or originating host.
2. Identify the affected user account.
3. Review the number and timing of failed authentication attempts.
4. Determine whether multiple accounts were targeted.
5. Check for a successful authentication following the failures.
6. Review the source host for additional suspicious activity.
7. Determine whether the behavior is legitimate or malicious.
8. Contain the source or account when required.

---

## Potential False Positives

Possible legitimate causes include:

- Users entering incorrect passwords
- Misconfigured applications or services
- Password managers using outdated credentials
- Scheduled tasks using expired credentials

---

## Evidence

The following screenshots document the current detection-engineering work:

### Brute Force Detection

`1 brute-force-detection.png`

The screenshot provides evidence of the brute-force detection use case and its associated security analysis.

### Active Directory Security Groups

`2-active-directory-security-groups.png`

The screenshot provides supporting evidence of the Active Directory security-group structure used by the lab environment.

---

## Current Status

**Phase 10 - Detection Engineering: In Progress**

The initial brute-force detection use case has been documented.

The detection has not yet been fully validated through a controlled attack simulation and centralized SIEM alert.

Future validation will include generating authentication failures in the lab and verifying that the resulting Windows security events can be detected and investigated.

---

## Next Steps

- Generate controlled failed authentication events.
- Verify Event ID 4625 on the Domain Controller.
- Verify successful authentication events when applicable.
- Forward authentication logs to the SIEM.
- Create and test a production-style detection rule.
- Document investigation results.
- Map validated detections to additional MITRE ATT&CK techniques.
