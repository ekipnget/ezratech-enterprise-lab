# DHCP Configuration

The ojective of this document is to configure Dynamic Host Configuration Protocol (DHCP) service to automatically assign IP address to client devices in EzraTech environment. By using DHCP administrators avoid manually configuring every workstation reducing errors and simplifying network management.

## Background

When a computer connects to the network, it needs network settings before it can communicate. DHCP automatically provides:

- IP address
- subnet mask
- Default gateway
- DNS server 
- Domain name

Without DHCP, each workstation would require manual configuration.

# DHCP Server information

Setting   |  Value
Server    |  DC01
Service   |  DHCP
Scope name|  EzraTech LAN
Network    | 192.168.10.0/24

# Install the DHCP server role

## Configuration

The DHCP server role was install using Server Manager. After installation, the server was authorized in Active Directory so it could begin leasing IP address.

## screenshot - DHCP role installed in server manager

## Validation
The DHCP appears under the installed roles.

# Authorize the DHCP server within Active Directory

Authorization prevents unathorized (rogue) DHCP servers from assigning IP addresses on the network.

# screenshot - Authorized DHCP server in the DHCP management console

## Validation

The server status changes to "Authorized"

# Configure the DHCP scope

Create a scope to define the range of IP addresses the can be assigned to client computers.

## Scope Configuration

Settings   |  Value
Scope name  |  EzraTech LAN
Start IP    |  192.168.10.100
End IP      |  192.168.10.200
Subnet Mask | 255.255.255.0

# screenshot - DHCP scope wizard

## Validation

The scope is active and ready to lease address.

## COnfigure DHCP options

Provide additional network settings to clients automatically.

## option 003 - Router

Default Gateway - 192.168.10.1

## Option 006 - DNS Server

192.168.10.10

## Option 015 - DNS Doman Name

corp.ezratech.local

# Screenshot -- DHCP scope options

## Validation

Clients successfily received the correct gateway, DNS server, and domain name.

# Configure Address Reservations

Reserve specific addresses for devices that should always receive the same address. Examples include: Network devices, NAS devices and Future application servers.

## screenshot -- DHCP recervation

## validation

Reserves devices always receive their assigned IP addresses.

# Test DHCP

Verify that windows 11 client successfuly receives its network configuration.

## Comands used

Release the current lease:

powershell - ipconfig /release

Request a new lease:

powershell - ipconfig /renew

Display the assinged configuration:

powershell: ipconfig /all

The client should receive:

- An IP address within the DHCP scope
- Subnet mask: 255.255.255.0
- Default gateway: 192.168.10.1
- DNS server: 192.168.10.10
- Domain name: corpezratech.local

# screenshot -- output of ipconfig /all  on windows 11 client

## Validation

The DHCP lease process follows the steps, commonly reffered to as "DORA"

1. Discover - The client broadcasts a request for DHCP Server.
2. Offer - The DHCP server offers an available IP address
3. Request - The client requests the offered address.
4. Acknowledge - The DHCP server confirms the lease.

## Validation

The DHCP deployment is considered successful when:

- Windows 11 clients automatically receive IP address.
- Clients receive the correct gateway, DNS server, and domain name
- Clients can commnicate withing the domain controller.
- clients can access the internet through pfSense.

# Key takeways

DHCP automates netwokr configuration, reduces administrative effort,and ensures consistent network settings across all client devices.


