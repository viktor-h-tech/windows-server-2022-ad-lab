# Windows Server 2022 Active Directory Home Lab

## Overview
This project documents a hands-on Windows Server 2022 home lab built to simulate a small enterprise Active Directory environment. The lab focuses on domain services, DNS configuration, organizational unit (OU) design, and user management using industry best practices.

## Security Objectives

This lab is evolving from a basic Active Directory deployment into a Blue Team detection lab.

Primary goals:

- Understand how authentication works in an AD environment
- Generate meaningful Windows security logs
- Ingest logs into a SIEM
- Build basic detection logic for:
  - Failed logon bursts (brute force)
  - Account lockouts
  - Privilege escalation (admin group changes)
  - New user account creation
- Practice documenting security events from detection to validation

This project simulates a small enterprise AD environment monitored by a SOC team.

## Environment
- Hypervisor: VMware Workstation
- Server OS: Windows Server 2022
- Domain: lab.local
- Server Name: DC01
- Network: NAT with static IPv4 addressing

## Planned Architecture (With SIEM)

The next phase introduces centralized log collection and monitoring:

- Windows Server 2022 (DC01)
- Windows 11 domain-joined client
- Dedicated SIEM VM (Wazuh planned)
- Windows Event Logs forwarded to SIEM
- Detection rules for authentication and account management events

## Architecture Diagram

    +------------------+
    |  WIN11-CLIENT    |
    +------------------+
             |
             | Domain Authentication
             v
    +------------------+
    |  DC01 (AD DS +   |
    |  DNS Server)     |
    +------------------+
             |
             | (Planned Log Forwarding)
             v
    +------------------+
    |  SIEM Server     |
    |  (Wazuh Planned) |
    +------------------+

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

### Server Manager – AD DS Installed
![Server Manager AD DS](screenshots/server-manager-ad-ds.png)

### Active Directory OU Structure
![AD OU Structure](screenshots/aduc-ou-structure.png)

### Static IPv4 and DNS Configuration
![Static IP DNS](screenshots/static-ip-dns.png)

### Domain Password Policy Enforcement
![Password Policy](screenshots/password-policy-enforcement.png)

## Windows 11 Client Integration

A Windows 11 client machine was added to the lab environment to simulate a real enterprise workstation joining an Active Directory domain.

## Client Configuration
- Client OS: Windows 11
- Machine Name: WIN11-CLIENT
- Joined Domain: lab.local
- Hypervisor: VMware Workstation
- Network: Host-only / NAT (VMnet) with domain-based DNS

## Key Tasks Completed
- Created a Windows 11 client VM
- Configured DNS on the client to point to the Domain Controller
- Resolved DNS and network profile issues preventing domain join
- Successfully joined the client to the `lab.local` domain
- Verified domain authentication using domain credentials (`lab\administrator`)

### Client Validation Screenshots

#### Confirmed DNS resolution using `ping lab.local`
![Client DNS Connectivity - ping](screenshots/client-dns-connectivity-ping.png)

#### Verified DNS name resolution using `nslookup`
![Client DNS Resolution - nslookup](screenshots/client-dns-resolution-nslookup.png)

#### Verified domain authentication context using `whoami`
![Domain Authentication - whoami](screenshots/client-domain-authentication-whoami.png)

This step completed the core Active Directory lab by demonstrating domain-joined client functionality.

## Status

✅ Core AD DS + DNS + Windows 11 domain join is complete. The lab environment is stable and documented with validation screenshots.

🚧 Current focus: transitioning this lab from “IT admin fundamentals” into a **SOC/Blue Team monitoring lab** by enabling Windows security auditing and integrating a SIEM.

## Current Roadmap (Next Phases)

**Phase 1 — Security Hardening + Logging (In Progress)**
- [ ] Enable Advanced Audit Policy on Domain Controllers (logon events, account management, group changes)
- [ ] Configure baseline domain security policies (account lockout, password policy review, least privilege)
- [ ] Create a tiered OU/admin structure (separate admin accounts from standard users)
- [ ] Create repeatable “attack simulation” tests to generate logs (failed logons, account lockouts, privilege changes)

**Phase 2 — SIEM Integration (Planned)**
- [ ] Deploy a SIEM (planned: **Wazuh** or Splunk Free) in a dedicated VM
- [ ] Install SIEM agents on DC01 and WIN11-CLIENT
- [ ] Forward Windows Event Logs (Security, System, etc.) into SIEM
- [ ] Create initial detections/alerts:
  - Failed logon bursts (brute force)
  - Account lockouts
  - New user created / user enabled
  - Admin group membership changes
- [ ] Document dashboards, detections, and validation results

## Current Challenge / Help Wanted

This lab is being resumed after a break, and I’m currently working through a **credential/access recovery + process hardening** step (password management + snapshots) to prevent future lockouts.  
If you have suggestions for best-practice auditing baselines, SIEM choice, or “must-have” Windows detections for a small enterprise AD environment, feedback is welcome.

## Process Improvements

- Importance of snapshotting before major configuration changes
- Importance of documenting domain admin + DSRM credentials securely
- Treating a home lab like production: logging, monitoring, and recovery planning

## Lessons Learned
- Importance of static IP and DNS configuration before promoting a Domain Controller
- How domain password policies override local expectations
- Common DNS and DHCP issues in NAT-based virtual environments
- Practical OU design for scalable user and computer management
