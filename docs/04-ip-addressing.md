# IP addressing Plan

This document defines the IP addressing scheme for the EzraTech enterprise infrastrucure.

A strucured IP addressing plan ensures that all devices communicate reliably while making network easier to manage, troubleshoot, and expand.

## Network information

Network Address | 192.168.10.0/24
Subnet Mask | 255.255.255.0
Default Gateway | 192.168.10.1
DNS server | 192.168.10.10
Broadcast Address | 192.168.10.255

# Why this subnet?

The 192.168.10.1/24 was selected because it provides up to 254 usable IP addresses hence allowing future expansion.

## Static IP address allocation

Infrastrucure devices should always have static IP addresses.
This ensures that critical services such as Active Directory and DNS are always reachable at predictable addresses.

Device                 | Hostname    |  IP Address
PfSense firewall       | PFSENSE01   |  192.168.10.1
Domain Controller      | DC01        |  192.168.10.10
File server            | FS01        |  192.168.10.20
Print server (Future)  | PRINT01     |  192.168.10.30

## DHCP scope

Employees will receive IP addresses automatically from the DHCP server.

# DHCP Scope

start address: 192.168.10.100
End Address:   192.168.10.200
Maximum clients: 

# Reserved IP addresses
The following IP addresses are reserved for the infrastrucure devices.
192.168.10.1 - 192.168.10.90 | Servers, Firewalls, Printers
192.168.10.100 - 192.168.10.200 | DHCP clients
192.168.10.201 - 192.168.10.254 | Future expansion

# Default gateway

All devices use 192.168.10.1. This is the LAN interface for pfSense Firewall. The default gateway allows internal devices to communicate with external networks such as the internet.

# DNS server

All domain-joined devices use: 192.168.10.10. The Windows server DC hosts the internal DNS service. This enables:
- Active directory authentication
- internal hostname resolution.
- Domain services.

# DHCP options

The DHCP server will automatically distribute:
-The default gateway 192.168.10.1
-DNS server 192.168.10.10
-Subnet Mask 255.255.255.0
-Domain Name corp.ezratech.local

# Future expansions

The  network design allows future additions, including:
- Additional domain controllers
- Application servers
- Linux servers
- Printers
- Network Attached Storage (NAS)
- Additional employee workstations





