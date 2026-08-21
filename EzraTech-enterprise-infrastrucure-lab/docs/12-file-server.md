# File server deployment

The objective of this document is to deploy a dedicated windows file server (FS01) to provide centralized, secure,and reliable file storage for EzraTech orgnization. The file server will intergrate with Active Directory to control access using Security groups, ensuaring employees only access files appropriate for their department.

# Background

As organization grow, storing files on individual compuiters becomes difficult to manage and increases the risk of data loss.

A dedicated file server includes:
- Centralized file storage
- Secure file sharing
- simplifies backups
- Centralized permissions
- improved collaboration
- Easier administration

Unlike the domain controller, the file server is dedicated to storing and managing company data.

# File server information

Server name - FS01
Operation system - Windows server 2022
IP address - 192.168.10.20
Domain - corp.ezratech.local
Primary role - File Server

# Why a separate server?
In production environment, Microsoft recommends seperating roles whenever possible. Separating the file server from the Domain controller provides several advantages:

- Improved security
- Better perfomance
- Easier troubleshooting
- Independent maintenance
- Greater scalability

This design follows common enterprise best practices

# Join FS01 to the domain

Before providing file sharing services, FS01 must become member of the EzraTech Active Directory domain.

# Configuration

Hostname - FS01
Domain - corp.ezratech.local
IP Address - 192.168.10.20
Preferred DNS - 192.168.10.10 (DC01)

# screenshot - system properties showing FS01 joined to the domain

# Validation

FS01 successfully joins the Active Direcotory domain and restarts without errors.

# Install the File Server Role

Install the File server role using server manager. This enables windows server to host shared folders and manage file-sharing services.

# screenshot - file server role installation in server manager

# Validation

The File Server role appears under installed roles.

# Create the shared folder strucure
A dedicated storage location was created on FS01.
Example: D:\Shares
Folder strucure:
D:\Shares
Public
HR
Finance
IT
Sales
Management

# Why seperate folders:?
Each department receives its own dedicated folder to ensure only employees access files required for their job responsibilities.

For example:
- HR stores employee records
- Finance stores accounting documents
- IT stores administrative scripts and documentation
- Sales stores customer proposals and contracts

# screenshot - folder strucure displayed in file explorer

# Configure share permissions

Share permissions control access when users connect over the network.

share   | security group   | Permission
Public    Domain users       Read
HR        HR_Users          
Finance   Finance_Users
Sales    Sales_Users
IT       IT_Admins
Management | Management   | Full control

# screenshot - advanced sharing permissions for the HR share

# Configure NTFS permissions
NTFS permissions protect the files stored on the server.

Folder     security group    permission
Public     Domain users      Read
HR         HR_Users          Modify
Finance    Finance_Users     Modify
Sales      Sales_Users       Modify
IT         IT_admins         Full control

## Why use both share and NTFS permissions?

Share permissions apply when users access folders over the network while NTFS permissions apply directly to the files and folders. The most resctrictive permission always applies.
For example, Share permissions > full control, NTFS permission > Read > effective permission. This layered security helps protect sensitive data.

# screenshot - NTFS security tab showing configuration 

# Test User Acess
The following users were used during testing

# Test user access

The following domain users were used during testing

User        deparment
Ezra        IT
Jane        HR
Michael     Finance
David       Sales

Testing confirmed:
- HR users scan access HR
- Finance users can access sales
- Sales Users can access sales
- IT administration have administrative access
- Unathorized users receive an "Access denied" message

# screenshot - successful acces to the HR share

# screenshot -  access denied to the HR share

# screenshot - Access denied when attempting to open unathorized share

# Map Network Drives

To simplify access for employees,shared folders were automatically mapped using group policy.
Example:
H: \\FS01\HR
F: \\FS01\Finance
S: \\FS01\Sales
P: \\FS01\Public

mapped drives automatically appear when users sign in.

# screenshot - mapped network drives displayed in windows file explorer

# Validation

Drive mappings appear automatically after domain login

# Testing
The follwing tests were completed

## Test 1
HR employee opens: \\FS01\HR
Expected result: Success

## Test 2

Finance employee opens: \\FS01\Finance
Expected results: Success

## Test 3

Sales employee attempts: \\FS01\Finance
Expected result: Access Denied

## Test 4

IT administrator creates a new folder inside the IT share.
Expected result: success

## Test 5

Mapped network drives appear automatically after user login.
Expected result: Success

# Security consideration

The file server deployment follows several security best practices.
- Dedicated server role
- Active directory authentication
- Security groups
- Share permissions
- NTFS permissions
- Priniciple of least privilege

This controls reduce unathorized access while simplifying administration.

# Key takeaways

Deploying a dedicated File server separates data storage from identity services, improving security, performance, and scalability. By intergarating FS01 with Active Directory security groups and group policy, the EzraTech environment provides centralized, secure, and efficient access to company data.





