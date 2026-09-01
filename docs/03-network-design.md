## Network Design

The objective of this document is to describe the logical network design for the EzraTech enterprise. A well designed network ensures secure communication between devices, simplifies administration, and provides foundation for future expansion.

The EzraTech network consists of a secure interal LAN protected by pfsense firewall. The firewall separates the internal network from the internet and controls all incoming and outgoing traffic.

The internal network contains:

- Windows server 2019 (Domain controller)\
- Windows 11 enterprise client
- File Server

The pfSense firewall provides: NAT services, Firewall protection, internet access, VPN connectivity and Traffic filtering.

# Network topology

    
## Internet

It represents the public network used for: Windows updates, package downloads, Remote VPN connections and General internet access.

## pfSense firewall 

It acts as the gateway between the internet and the internal network. It protects internal devices, filters network traffic, performs NAT services, Hosts OpenVPN server and routes traffic between networks.

## Domain Controller (DC01)

Primary services includes: Active directoty Domain services, DNS, DHCP, Group policy and authentication.

## Windows 11 client (PC01)

it represents an employee workstation. it's functions includes: joining the AD Domain, receiving IP address from DHCP, Logging in using Domain credetials, Assesing shared resources and connecting to the internet through pfSense.

## Netwrok Traffic flow

When a user opens a web browser in windows 11 client, the following process occurs:

1. The client sends traffic to the dafault gateway (pfSense).
2. pfSense examines the firewall rules. 
3. if the traffic is permitted, pfSense performs NAT.
4. The traffic is forwarded to the internet.
5. Responses return through pfSense before reaching the client.

## Why PfSense was selected?

It provides enterprise-grade firewall functinality, VPN support, NAT, DHCP services (If required), and advanced traffic monitoring.

## Why seperate the Doman Controller?

Separating Active Directory from the firewall improves security, reliability, and manageability.

## Why Host-Only Networking? 

It allows the windows server and windows client to communicate privately through pfSense without exposing internal network directly to physical network.




         
