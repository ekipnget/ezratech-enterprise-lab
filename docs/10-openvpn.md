# openVPN Deployment

The objective of this document is to deploy openVPN on the pfSense firewall to provide a secure remote access to the EzraTech internal network. Employees working remotely will be able to securely access company resources, including Active Directory services , shared folders, and internal applications, over an encrypted VPN tunnel.

# Background

Remote employees require secure access to internal resources. Rather than exposing internal servers directly to the internet, OpenVPN creates an encrypted tunnel between the employee's computers and the EzraTech network. All data transmitted through the VPN is encrypted using TLS certificate, protecting it from interception. 

## VPN Architecture

# Why OpenVPN?
OpenVPN was selected because it provides:

- Strong encryption
- Certificate-based authentication
- cross-platform compaatibility
- secure remote administration
- intergration with pfSense

# Create a Certificate Authority

Create an internal certificate authority used to sign the VPN certificates. The certificate authority establishes trust between the VPN server and VPN clients.

## Configuration

certificate authority name - EzraTech-CA
Algorithm - RSA 4096-bit
Hash algorithm - SHA 256
Lifetime - 3560 Days

# screenshot - Certificate Authority created in PfSense

## Validation

The certificate authority appears in the pfSense certicate manager

# Create the openVPN server certificate

This certificate identifies the VPN server to connecting clients.

## screenshot of server ceriticate

## Validation - the certificate is successfully issued by EzraTech-CA

# COnfigure the OpenVPN Server

The objective is to deploy the OpenVPN server within pfSense.

## Configuration

Protocol - UDP
Authentication - TLS certificate
Tunnel Network - 10.8.0.0/24
Local network - 192.168.10.0/24
DNS server - 192.168.10.10
 
## screenshot - OpenVPN server configuration

## Validation

The VPN server start successfully.

# Create VPN Users

This is to allow authrized employees to authenticate to VPN.

Example users:

-Ezra, Jane, David

Each user receives: Username, password and client certicate

# Screenshot of VPN  user accounts

## Validation

Users are associated with valid VPN certificate

# Configure firewall rules

Firewall rules permit: OpenVPN, DNS, Internal network

Only authenticated users are allowed access.

## VPN traffic passes through the firewall

# Export client configuration

Generate client configuration files.

The exported package contains: client certificate, private key and VPN settings

Examples file: Ezra.ovpn

# screenshot -  openVPN client export utility

## validation

configuration files are successfully generated.

# Connect a windows client

The objective is to verify that windows client can establish a VPN connection.

Steps

1. install openVPN connect
2. import the .ovpn file.
3. connect to the VPN.
4. Authenticate.
5. Verify connectivity.

# screenshot of OpenVPN client connected successfully.

## Validation

The client receives a VPN IP addresses.

# Testing

The following tests were perfomed:

## Test 1
ping DC01
Result: Successful

## Test 2
Open shared folder
Result: Accessble

## Test 3
Run  nslookup DC01
Result: DNS resolution

## Test 4

Browse internal resources
Result: Successfull

# Security consideration

The VPN deployment follows several security best practices.

- Certificate-based authentication
- Enrypted communication
-Strong encryption algorithms
- Firewall protection
- Restricted user access
- Least privilege principle

# Validation

The VPN deployment is considered successful when:

- Remote users authenticate successfully
- Internal resources are accessible.
- Traffic is encrypted.
- DNS resulution functions correctly.
- Firewall logs show successful VPN sessions.

# Key Takeaways

OpenVPN provides secure remote connectivity by combining strong encryption, certificate-based authentication, and firewall protection.

This deployment enables employees to work securely from remote locations while maintaining access to internal company resources.





