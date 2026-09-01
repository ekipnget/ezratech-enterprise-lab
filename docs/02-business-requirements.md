# Business requirements

## purpose

This document defines the technical and business requirements for EzraTech enterprise infrastucure deployment.

The objective is to build a secure, scalable and manageable network that supports approximately 50 employees while following industry best practices.

# Functional requirents

The infrastrucure must provide the following services:

## 1. Identity Management

The enviroment shall provide centralized authentiction using Active Directory Domain Services.

Requirements:

- Create a single Active Directory domain
- Authenticate users and computers
- Organize Users to Organizatinal units
- Use security Groups for access control

## 2. DNS Services

The infrastrucure shall provide interal DNS services.

Requirements:

- Forward Lookup Zone
- Reverse Lookup Zone
- Internal hostname resolution
- Domain controller name resolution

## 3. DHCP Services

The infrastrucure shall atomatically assign IP addresses to client computers.

Requrements:

- Configure a DHCP scope
- Assign the correct subnet mask
- Configure DNS Server
- Reserve static IP addresses for servers

## 4. Network Security

The network shall be protected using pfsense firewall.

Requirements:

-secure LAN and WAN interfaces
-configure NAT
-create firewall rules
-restrict unathorized traffic
-monitor network traffic

## 5. Remote access

Authorized employees shal be able to securely connect from outside the office.

Requirements:

- Configure OpenVPN
- Create VPN user accounts
- Use cerificate-based authentication
- verify remote connectivity

## 6. Group policy

Administrators shall contrally manage windows computers.

Requirements:

- Password policy
- Account Lockout
- Windows Update policy
- Deskstop configuration
- Security settings

## 7. File Servers

The environment shall provide centralized file storage.

Requirements:

- Deparment shared folders
- NTFS permissions
- Security Group access
- Shared network drives

#  Non-Functional requirents

The solution should also meet the following objectives.

## Security

-Centralized authentication
- least privilege access
- strong password policy
- firewall protection

## Reliability

- stable DNS servies
- Relaible DHCP
- Consistent user authentication

## Scalability

The infrastrcure should support future growth beyond 50 employees.

# Success Criteria

The project will be considered successful when:

- Windows 11 clients successfuly join the domain.
- Users cna log in using Active Directory Accounts.
- DNS resolves internal hostnames.
- Internet traffic passes through pfSense.
- OpenVPN clients can securely connect.
- Group policies are successfully applied.
- Users can access shared folders according to their permissions.






