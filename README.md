# Windows Server 2022 Active Directory Home Lab

## Overview
This project documents a hands-on Windows Server 2022 home lab built to simulate a small enterprise Active Directory environment. The lab focuses on domain services, DNS configuration, organizational unit (OU) design, and user management using industry best practices.

## Environment
- Hypervisor: VMware Workstation
- Server OS: Windows Server 2022
- Domain: lab.local
- Server Name: DC01
- Network: NAT with static IPv4 addressing

## Key Features Implemented
- Installed and configured Active Directory Domain Services (AD DS)
- Promoted server to Domain Controller
- Configured DNS integrated with AD
- Assigned static IPv4 address following DC best practices
- Created Organizational Units:
  - Lab_Users
  - Lab_Computers
  - Lab_Admins
- Created and managed domain user accounts
- Enforced domain password policies
- Troubleshot DNS and DHCP conflicts in a virtualized environment

## Skills Demonstrated
- Active Directory (AD DS)
- Windows Server 2022 Administration
- DNS Configuration
- Group Policy Fundamentals
- Virtualization (VMware)

## Screenshots

> Screenshots documenting key configuration steps and validation.

- Server Manager dashboard after AD DS installation
- Active Directory Users and Computers (OU structure)
- Domain user creation and password policy enforcement
- Network configuration (static IPv4 & DNS)

## Status
🚧 Ongoing — future additions will include Group Policy Objects (GPOs), additional client machines, and security hardening.

## Lessons Learned
- Importance of static IP and DNS configuration before promoting a Domain Controller
- How domain password policies override local expectations
- Common DNS and DHCP issues in NAT-based virtual environments
- Practical OU design for scalable user and computer management
