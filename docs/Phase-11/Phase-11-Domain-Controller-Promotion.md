# Phase 11 - Domain Controller Promotion

## Objective

Promote the Windows Server VM to the first Domain Controller for the Enterprise SOC Lab and verify that Active Directory Domain Services and DNS are functioning correctly.

---

## Environment

| Component | Configuration |
|---|---|
| Domain Controller | DC01 |
| Domain | enterprise.local |
| Role | Active Directory Domain Controller |
| DNS | Windows Server DNS |
| Network | Enterprise isolated lab network |

---

## Domain Controller Promotion

The Windows Server system was promoted to a Domain Controller for the `enterprise.local` Active Directory domain.

The promotion established the server as the central authentication and directory-services system for the lab environment.

---

## Active Directory Verification

After promotion, Active Directory Users and Computers was opened to verify that the domain directory was available.

The Active Directory Administrative Center was also used to verify administrative access to the domain.

---

## DNS Verification

The DNS forward lookup zone for the Active Directory domain was verified after Domain Controller promotion.

Active Directory depends on DNS for domain discovery and authentication services, so DNS functionality was validated as part of the Domain Controller deployment.

---

## Domain Verification

The domain configuration was verified after promotion to confirm that the Domain Controller was operating within the expected Active Directory environment.

---

## DCdiag Validation

The `dcdiag` diagnostic utility was used to validate the Domain Controller.

The successful diagnostic result provides evidence that the Domain Controller passed the documented health checks performed during this phase.

---

## Evidence

The following screenshots document the Domain Controller deployment and validation:

1. `1-domain-controller-promoted.png`
2. `2-active-directory-users-and-computers.png`
3. `3-dns-forward-lookup-zone.png`
4. `4-administrative-center.png`
5. `5-domain-verification.png`
6. `6-dcdiag-success.png`

---

## Result

The Windows Server VM was successfully promoted to a Domain Controller and the available Active Directory and DNS functionality was verified.

---

## Status

**Completed**

Phase 11 Domain Controller deployment and validation is complete based on the available lab evidence.
