# Phase 11 - Windows Server Rebuild

## Objective

Document the Windows Server rebuild performed during the Enterprise SOC Lab deployment and the subsequent restoration of the Domain Controller environment.

---

## Rebuild Context

The Windows Server VM was rebuilt as part of the lab infrastructure deployment.

The rebuild provided a clean Windows Server environment for the Active Directory Domain Controller configuration.

---

## Domain Controller Configuration

Following the rebuild, the Windows Server environment was configured for the Enterprise SOC Lab Active Directory domain.

The resulting Domain Controller environment was validated through:

- Active Directory Users and Computers
- DNS forward lookup zone
- Active Directory Administrative Center
- Domain verification
- Domain Controller diagnostics

---

## Validation

The successful Domain Controller promotion and `dcdiag` validation provide evidence that the rebuilt Windows Server environment was successfully integrated into the Active Directory lab.

---

## Evidence

The detailed validation evidence is documented in the Phase 11 Domain Controller Promotion screenshots.

---

## Result

The rebuilt Windows Server environment was successfully used to establish and validate the Enterprise SOC Lab Domain Controller.

---

## Status

**Completed**

The Windows Server rebuild and subsequent Domain Controller validation were completed as part of the lab deployment.
