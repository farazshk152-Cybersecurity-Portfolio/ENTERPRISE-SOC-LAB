# Phase 5 - Enterprise Network Configuration

## Objective

Configure the networking for the Enterprise SOC Lab.

This phase prepares the environment for:

- Active Directory
- DNS
- Windows Client
- Kali Linux
- Wazuh SIEM

The goal is to create an isolated enterprise network where all virtual machines can communicate securely.

## Current Status

- VirtualBox installed
- Windows Server 2022 installed
- Active Directory Domain Services installed
- DNS Server installed
- Preparing to configure networking before promoting the server to a Domain Controller.

## Network Design

The Domain Controller is configured with two virtual network adapters.

### Adapter 1

- Type: NAT
- Purpose: Internet access for downloading software and updates.

### Adapter 2

- Type: Internal Network
- Network Name: SOC-LAB
- Purpose: Communication between all virtual machines inside the isolated enterprise environment.

This dual-adapter configuration simulates a production-style enterprise network while keeping the lab isolated from the home network.

# Network Adapter Verification

After adding a second virtual network adapter in virtualbox, Windows server detected two network interfaces:

-Adapter 1 (NAT) for internet connectivity
-Adapter 2 (Internal Netowrk - SOC-LAB) for communication between virtual machines.

this configuraton mirrors a common enterprise development where management/internet access is separated from internal network. 
