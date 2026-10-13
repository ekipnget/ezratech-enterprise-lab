## DNS configuration

The objective of this document is to configure the Domain Name System (DNS) service for the EzraTech Active Directory environment.

DNS enables computers to locate domain controllers, resolve hostnames, and communicate with network resources efficiently.

# Background

AD depends heavily on DNS. When a user signs in to a domain, the client first contacts the DNS server to locate a Domain Controller.

Without a properly configured DNS service:

- Computers cannot join the domain.
- Users cannot authenticate
- Group policy fails
- Active Directory services become unavailable

# DNS server information

server name - DC01
Role - DNS server
IP address - 192.168.10.10
Domain - corp.ezratech.local

# Forward Lookup Zone

A forward Lookup zone resolves hostnames to IP addresses.
Example: 
Dc01.corp.ezratech.local > 192.168.10.10

## Configuration

A forward Lookup Zone was created for:

corp.ezratech.local. The zone stores DNS records for all domain joined devices.

## screenshot showing forward lookup zone displayed in DNS manager

# Reverse Lookup Zone

A reverse Lookup Zone resolves IP addresses back to hostnames.

Example:
192.168.10.10 > DC01.corp.ezratech.local

## Configuration

A Reverse Lookup Zone was created for the subnet:
192.168.10.0/24

## screenshot of Reverse Lookup Zone displayed in DNS Manager

# Host A records

Host A records maps hostnames to IPv4 addresses.
Example: DC01 > 192.168.10.10

## Records created

Hostname       IP address
DC01           192.168.10.10
PC01           Assingned by DHCP

# screenshot DNS manager displaying host A records

## SRV records

SRV records alloe clients to locate Active Directory services automatically.

Examples: Kerberos, LDAP, Global catalog

The records are created automatically when the Domain Controller is promoted.

# screenshots srv records 

## DNS forwarders

DNS forwarders allow unresolved external requests to be forwared to an external DNS server.

Example: 
- 8.8.8.8
- 1.1.1.1

This enables internal clients to resolve internet domain names.

## screenshot of DNS forwaeders configuration

## validation
Clients can resolve both internal and external hostnames.

# DNS testing
## Test 1
Command:
nslookup DC01 
results: returns 192.168.10.10

## Test 2
Command:
nslookup corp.ezratech.local
results: returns the Domain Controller.

## Test 3
command:
ping DC01
results: Hostname resolves successfuly.

## Test 4
command:
ipconfig /displaydns
results: Displays cached DNS entries.

# Common DNS problems

Problem    |  Possible cause
Domain join failed | Wronf DNS server configured
Name resolution failed | Missing A record
Cannot log in  | DNS service unavailable
Group policy Errors | client cannot locate the Domain controller

# Validation

The DNS deployment is considered successful when:
- clients resolve internal hostnames.
- clients resolve internet hostnames.
- AD authentication succeeds
- nslookup returns expected results.
- Reverse lookups function correctly

