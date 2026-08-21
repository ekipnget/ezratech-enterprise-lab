# PfSense firewall deployment

The abjective of this document is to deploy and configure pfSense firewall for the EzraTech enterprise netowork. The firewall provides secure communcation between the internal network and the internet while enforcing security policies, performing NAT services and supporting secure remote access.

# Background

A firewall is the first line of defense for a network. Instead of allowing every computer to connect directly to the internet, all traffic passes through the firewall where it can be  inspected, filtered, logged, and controlled.

In this lab, pfSense acts as:

- Default gateway
- Firewall
- Router
- NAT device
- VPN gateway

# Firewall information

setting    |  Value
Hostname   |  PFSENSE01
OS         |  PfSense commnity Edition
LAN IP address |  192.168.10.1
WAN interface  |  DHCP (VirtualBox NAT)
LAN interface  | Host-only network

## Network Architecture

Why 2 network adapters?

The pfSense firewall requires 2 network interfaces.

## WAN adapter

The WAN adapter provides internet connectivity.

VirtualBox Adapter:

NAT, Why NAT? The WAN interface needs internet access through host computer.

## LAN adapter

LAN adapter provides connectivity to the internal EzraTech network.

VirtualBox Adapter:

Host-only, why Host-only? The internal network should remain isolated while allowing commnication between pfSense, Windows Server, and Windows 11.

# Initial Configuration

After  installation, the following interfaces were assigned:

WAN - vtnet0

LAN - vitnet1

The LAN interface was configured with: 192.168.10.1/24

# Verify network connectivity

The following tests were performed:

## Test 1 - ping the Domain contoller
Result: successful

## Test 2 - ping the windows 11 client
Result: Successful

## Test 3 - ping the external IP address
example 8.8.8.8
Result: Successful

## Test 4 - Browse the pfSense web interface
https://192.168.10.1
Result: Dashboard loads successfuly.

# Firewall rules

The defauth firewall rules were reviewed. Additional rules were created as required to allow:
DNS, DHCP, HTTP, HTTPS, and OpenVPN

Each rule follows the principle of least privilege by allowing only the traffic required for business operations.

# Network Address Translation

This allows multiple internal devices to share a single internet connection. 
Example:
Before NAT, PC01 192.168.10.101 > internet (not routable)
After NAT, PC01 > PfSense > Host public IP > internet
The internet only sees the public IP assigned to WAN interface.

# DNS Configuration

Internal clients use: 192.168.10.10
Windows server DNS
PfSense forwards external DNS queries to public DNS servers when required.

# DHCP Considerations

Although  pfSense is capable of acting as a DHCP server, DHCP services are provided by windows server in this environment. This approach ensures tighter intergration with Active Directory and follows common enterprise deployment practices.

## Validation

The firewall deployment is considered successfull when:

- WAN has internet connectivity
- LAN devices communicate correctly.
- Windows 11 access the Internet
- The pfSense web interface is accessible.
- Internal traffic passes through the firewall.

