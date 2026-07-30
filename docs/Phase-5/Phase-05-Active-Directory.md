    # Phase 05 – Active Directory Deployment

## Objective

Install Active Directory Domain Services (AD DS) on DC01 and promote the server to the first Domain Controller for the Enterprise SOC Lab.

---

## Why Active Directory?

Active Directory provides centralized identity and access management.

It enables:

- User Authentication
- Computer Authentication
- Group Policy
- Organizational Units (OUs)
- Security Groups
- Centralized Administration

---

## Planned Domain

soclab.local

---

## Planned Forest

New Forest

---

## Planned Domain Controller

DC01

---

## Status

🟡 In Progress

## Server Roles Evaluated

| Role | Decision | Reason |
|------|----------|--------|
| Active Directory Domain Services | Install | Centralized identity and authentication |
| DNS Server | Install (dependency) | Required for Active Directory name resolution |
| DHCP Server | Not Installed | Static addressing will be used in the lab |
| Hyper-V | Not Installed | VirtualBox is the virtualization platform |
| Web Server (IIS) | Not Installed | Not required for this project |
| WSUS | Not Installed | Not required for this lab |

## Required Management Features

Active Directory Domain Services requires several supporting management tools.

### Installed Components

- Group Policy Management
- Remote Server Administration Tools (RSAT)
- AD DS and AD LDS Tools
- Active Directory Module for Windows PowerShell
- Active Directory Administrative Center

### Why They Are Required

These components provide the graphical interfaces and command-line tools needed to administer Active Directory and Group Policy within an enterprise environment.

### SOC Analyst Perspective

Administrative tools themselves are not malicious. However, attackers who gain privileged access may abuse them to create accounts, modify group memberships, reset passwords, or change policies. Monitoring administrative actions is therefore an important part of Windows security monitoring.

## Domain Controller Promotion

After installing Active Directory Domain Services, Windows Server requires promotion to a Domain Controller.

This process creates the Active Directory database and enables the server to provide authentication, authorization, DNS integration, and centralized identity management.

At this stage, the promotion wizard has been launched and the deployment configuration is ready to be completed.