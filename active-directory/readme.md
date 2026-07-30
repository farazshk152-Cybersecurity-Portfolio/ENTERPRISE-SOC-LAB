# Active Directory Installation

## Objective

Install Active Directory Domain Services (AD DS) and DNS Server to prepare the Windows Server VM to function as the Enterprise Domain Controller.

## Installed Roles

- Active Directory Domain Services
- DNS Server
- Group Policy Management

## Result

The required Windows Server roles were installed successfully and the server was prepared for promotion to a Domain Controller.

## Roles Installed

- Active Directory Domain Services (AD DS)
- DNS Server
- Group Policy Management
- Remote Server Administration Tools (RSAT)

These roles prepare the server to become the first Domain Controller for the Enterprise SOC Lab.

## Installation Notes

During installation, Windows displayed a warning indicating that no static IP address was configured.

This warning is expected because the server was temporarily using DHCP.

The static IP address will be configured before promoting the server to a Domain Controller to ensure reliable DNS and Active Directory functionality.

