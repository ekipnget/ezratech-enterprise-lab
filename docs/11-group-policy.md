EzraTech has 50 employees

Imagine the CEO says:

- Every computer should have our company wallpaper
- Everyone must use strong passwords
- HR should not be able to access control panel
- IT should automatically map the company file server

of course you dont want to visit computers. You create one group policy, and windows distributes it automaticall. That's the power of group policy. (GPO)

# Group policy configuration

The objective of this document is to configure Group Policy Objects (GPOs) to centrally manage security settings, user configurations, and computer policies within the EzraTech Active Directory environment.

Group Policy ensures that all domain-joined computers follow consistent security and operational standards.

# Background

Without group policy, adminstrators would need to configure every computer individually. By applying policies through Active Diretory, changes are automatically enforced across all domain-joined computers.

This approach improves:

- Security
- Standardization
- Complaince
- Administrative efficiency

# Group Policy Architecuture

Administrator > Domain controller (DC01) > Active Directory > Group policy > Windows 11 client

# Policy 1 - Password policy

The objective is to enforce passwords for all domain users.

## Configuration

Minimum password length - 12 characters
Complexity requirement - Enabled
Maximum password age - 90 days
Minimum password age - 1 day
Password history - 24 passwords

## Why strong passwords
This reduces the risks of:

- Password quessing
- Brute-Force attacks
- Credentials reuse

## screenshot of password policy setting in Group management

# validation

Users are required to create strong passwords.

# Policy 2 - Account Lockout Policy

The objective is to protect user accounts from repeated login attempts.

# Configuration

Lockout Threshold - 5 Failed Attempts
Lock out Duration - 15 Minuites
Reset Counter After - 15 Minutes

## Why?
Account lockout helps protect against brute-force attacks.

## screenshot - Account lockout policy

## Validation
Accounts lock after five login attempts.

# Policy 3 - Company Desktop Wallapaper

The objective is to apply EzraTech company wallpaper to all employee workstation.

# Configuration

wallpaper location
\\\\DC01\\wallpapers\\EzraTech.jpg
wallpaper style - Fill

# Why?  
A standardized desktop improves branding and helps verify that a workstation is managed by the organization.

# screenshot - windows 11 desktop displaying the EzraTech Wallpaper

# Validation
The wallpaper is automatically applied after Group policy updates.

# Policy 4 - Disable control panel

The objective is to prevent standard users from from changing important system settings.

## Why
Restricting access reduces accidental configuration chanages and improves security.

# screenshot - control panel restriction policy

## Validation
Standard users cannot open control panel

# Policy 5 - Windows update policy

The objective is to configure windows update settings for domain computers.

## Configuration
Automatic updates - Enabled
Installation Schedule - Every Sunday at 2:00AM

# screnshot- windows uppdate group policy

# Validation
Windows update settings are applied to domain clients.

# Applying group policy
After creating a group policy, the client computer was updated using:

In poweshell run - gpupdate /force

# Verifying Applied Policies
The following command was used to verify that policies were successfully applied.

In powershell run - gpresult /r  > the output confirmed that the expected Group policy Objects were applied to the Windows 11 Client.

# Testing
The following tests were performed

## Test 1
Attempt to use weak password.
Expected result - password rejected

# Test 2
Attempt five failed logins.
Expected result - Account becomes locked.

# Test 3 
Run gpupdate /force
Expected result - policies update successully.

# Test 4
Run -  gpresult /r
Expected result - Applied GPOs are displayed.

# Validation
The group policy deployment is considered successful when:
- Password policies are enforced.
- Account locout functions correctly.
- Company wallpaper is applied.
- Control panel restrictions are enforced.
- Group policy updates successfully on client computers.

# Key takeways
Group Policy enables centralized management of windows environments by automatically applying security and configuration settings to all domain-joined computers. This reduces administrative effort while ensuring consistent security and compliance accross the organzation.




