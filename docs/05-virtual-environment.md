# Lab Environment

This document describes the virtualization environment used to build the EzraTech enterprise infrustrucure lab.

The lab was buid using Oracle VM. Virtulization allows multiple operating systems to run on a single physical computer while remaining isolated from one another. This approach reduces hardware costs, simplifies testing and provides safe environment for learning and experimentation.

# Host machine

The host computer provides the hardware required to run all virtual machines.

Host operatin system | Windows 11
Virtulization Platform | Oracle VirtualBox
Internet Connection | Physical Network

# Virtual Machines

The EzraTech lab consists of 3 primary VMs.

## 1. pfSense Firewall
It serves as the perimeter network between the internet and the internal corporate network.

### Configuration

Hostname => PFSENSE01
Operating System => pfsense CE
CPU => 2vCPUs
Memory => 2GB
Storage => 20GB
Adapter 1 => NAT (WAN)
Adapter 2 => Host-only (LAN)

## 2. Windows Server 2019

The windows server hosts the core infrastrucure services.
This include: Active Directory Domain services, DNS,  DHCP, File servers and Group policy

### Configuration

Hostname | DC01
Operating System | Windows server 2019
CPU | 2 vCPUs
Memory | 4 GB
Storage | 80 GB
Network | Host-Only

## 3. Windows 11 enterprise

This VM represents a company employee workstations.
It is used to: Join the Active Directory Domain, Receive an IP address using DHCP, Test the group policy, Verfy DNS functionality and access shared folders.

### Configuration

Hostname | PC01
Operating system | Windows 11 enterprise
CPU | 2 vCPUs
Memory | 4 GB
Storage | 60 GB
Network | Host-only

# Virtual Network Configuration

The environment uses 2 virtualBox types.

## NAT network

The NAT adapter provides internet access to the pfSense WAN interface. This allows:

-Windows updates
- Package downloads
- Internet browsing
- VPN testing

## Host-Only Network

The Host-Only Network simulates EzraTech's internal LAN.
 Devices connected to this network include:

 -DC01
 -PC01
 -pfSense LAN interface

 # Why Virtualization

 - safe testing environment
 - snapshot capability
 - Easy recovery
 - Enterprise simulation
 - Repeatble deployments

 # Keys takeaways

 The Virtulization platform provides the flexible and isolated environment for designing, deploying, and testing, and troubleshooting enterprise infrastrucure without requiring physical servers.

 