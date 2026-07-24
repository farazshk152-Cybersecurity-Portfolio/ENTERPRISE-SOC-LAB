# Enterprise Architecture Overview

The Enterprise SOC Lab consists of four primary systems:

- DC01 (Windows Server)
- CLIENT01 (Windows 11)
- WAZUH01 (Ubuntu Server)
- KALI01 (Kali Linux)

All systems communicate through an isolated VirtualBox internal network.

Security events generated on Windows systems are collected by Wazuh for monitoring and investigation.

Kali Linux is used to simulate attacker behavior.