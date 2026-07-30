# Phase 04 – Windows Server Deployment

## Objective

Deploy the first virtual machine that will serve as the Domain Controller (DC01) for the Enterprise SOC Lab.

---

## Why Windows Server?

Windows Server provides enterprise services such as:

- Active Directory Domain Services (AD DS)
- DNS
- Authentication
- Authorization
- Group Policy

It acts as the central identity platform for the entire environment.

---

## Planned Configuration

| Setting | Value |
|---------|-------|
| Hostname | DC01 |
| Operating System | Windows Server 2022 Evaluation |
| Role | Domain Controller |
| RAM | 3072 |
| CPU | 2 vCPUs |
| Disk | 50 GB Dynamic VDI |

---

## Status

🟡 In Progress

---

# Virtual Machine Specifications

| Setting | Value | Reason |
|---------|-------|--------|
| VM Name | DC01 | Enterprise naming convention |
| Operating System | Windows Server 2022 Evaluation | Domain Controller |
| Generation | VirtualBox |
| Memory | 3072 MB | Optimized for 8 GB host RAM |
| CPUs | 2 | Good balance of performance |
| Video Memory | 64 MB | GUI only |
| Disk | 50 GB (Dynamic) | Saves host disk space |
| Network | NAT (initially) | Internet access during installation |

---

## Why these specifications?

The host system has 8 GB RAM and limited free SSD space.

The VM is configured to provide a smooth experience while leaving sufficient resources available for the host operating system.

---

# Installation Process

## Selected Edition

Windows Server 2022 Standard Evaluation (Desktop Experience)

## Installation Type

Custom Installation

## Virtual Disk

50 GB Dynamic VDI

## Installation Notes

The server was installed manually to gain familiarity with the Windows Server deployment process. Manual installation also provides better understanding of enterprise deployment workflows compared to unattended installations.

## Status

🟡 Installing


---

# Initial Administrator Configuration

The built-in Administrator account was configured during the first boot of Windows Server.

## Notes

- A strong password meeting Windows complexity requirements was configured.
- This account will be used for initial server configuration before Active Directory is deployed.

> **Note:** The actual password is **not documented** in this repository for security reasons.

---

# Computer Naming

## Hostname

DC01

## Naming Convention

| Prefix | Meaning |
|---------|---------|
| DC | Domain Controller |
| CL | Client Workstation |
| KALI | Attack Machine |
| WAZUH | SIEM Server |

Using standardized hostnames improves asset identification, log analysis, and incident response in enterprise environments

Computer Name 

Status : Completed

Hostname : DC01

the server restart was completed successfully and the new hostname was verified in server manager.

---

# Time Zone Configuration

## Selected Time Zone

UTC +05:30

Chennai, Kolkata, Mumbai, New Delhi

## Reason

Correct timestamps are essential for:

- Event Log Analysis
- SIEM Correlation
- Incident Response
- Threat Hunting

---

# Static IP Configuration

## Objective

Configure a static IPv4 address for the Domain Controller.

## Why Static IP?

A Domain Controller must always be reachable at the same IP address because:

- Active Directory depends on DNS.
- Client systems locate domain services through DNS.
- SIEM agents require consistent connectivity.
- Group Policy processing relies on reliable communication.
- Stable IPs simplify troubleshooting and incident response.

## Planned Enterprise Addressing

| Host | Planned IP |
|------|------------|
| DC01 | 192.168.100.10 |
| CLIENT01 | 192.168.100.20 |
| WAZUH | 192.168.100.30 |
| KALI | 192.168.100.40 |

> During the initial deployment, the VM remains on VirtualBox NAT. It will later be migrated to an isolated Internal Network (`SOC-LAB`) using the addressing scheme above.

---

# Network Configuration Discovery

## Objective

Identify the current DHCP configuration before assigning a static IP address.

## Commands Used

```cmd
ipconfig /all
```

## Purpose

The output will be used to identify:

- Current IPv4 Address
- Subnet Mask
- Default Gateway
- DNS Server

This information ensures the static IP configuration remains compatible with the current VirtualBox NAT network during the initial deployment phase.

---

# Network Adapter Configuration

## Adapter Name

Enterprise-LAN

## Reason

Network adapters should have descriptive names instead of generic labels such as "Ethernet".

Benefits:

- Easier troubleshooting
- Better documentation
- Consistent enterprise naming
- Simplified network administration