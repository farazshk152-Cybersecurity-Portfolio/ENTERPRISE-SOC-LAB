# Brute Force Detection

## Objective

Detect repeated failed login attempts that may indicate password guessing or brute force attacks.

---

## MITRE ATT&CK

Technique: T1110 – Brute Force

---

## Windows Event IDs

4625 – Failed Logon

4624 – Successful Logon (used to determine if the attack eventually succeeded)

---

## Data Sources

- Windows Security Logs
- Active Directory Logs
- Sysmon (optional)

---

## Detection Logic

Trigger an alert when:

- Multiple failed logon events occur from the same source
- Multiple usernames are targeted
- A successful logon follows repeated failures

---

## Severity

High

---

## Investigation Steps

1. Identify the source IP.
2. Determine the affected account.
3. Review the number of failed attempts.
4. Check whether a successful login occurred.
5. Determine if the activity is malicious or expected.
6. Contain the source if required.

---

## False Positives

- Users forgetting passwords
- Misconfigured services
- Password managers repeatedly trying old credentials

---

## Future Lab Validation

This detection will be validated by generating failed login events in the Enterprise SOC Lab after Active Directory is deployed.