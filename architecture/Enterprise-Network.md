# Enterprise Network Design

## Objective

Design a secure and isolated enterprise network for attack simulation, detection engineering, and incident response.

---

## Components

### DC01

- Windows Server 2022
- Active Directory
- DNS

---

### CLIENT01

- Windows 11 Enterprise
- Sysmon
- Wazuh Agent

---

### WAZUH01

- Ubuntu Server
- Wazuh Manager
- Dashboard

---

### KALI01

- Kali Linux
- Attack Simulation

---

## Network Type

Internal Network

This configuration isolates the lab from the physical network while allowing communication between all virtual machines.

---

## Benefits

- Safe malware testing
- Enterprise simulation
- Controlled attack environment
- Centralized log collection