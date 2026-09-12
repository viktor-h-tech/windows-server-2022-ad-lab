# Build and Validation Runbook

This runbook documents the completed, recruiter-visible portion of the Active Directory home lab. It intentionally separates validated configuration from the upcoming monitoring phase.

## Environment

| Component | Configuration |
|---|---|
| Hypervisor | VMware Workstation |
| Domain controller | Windows Server 2022 — `DC01` |
| Domain | `lab.local` |
| Client | Windows 11 — `WIN11-CLIENT` |
| Network | NAT / VMnet with static IPv4 addressing |

## Build summary

1. Install Active Directory Domain Services on `DC01`.
2. Promote `DC01` as the domain controller for `lab.local`.
3. Configure static IPv4 addressing and AD-integrated DNS on the domain controller.
4. Create OUs for users, computers, and administrators.
5. Create test domain identities and apply domain password-policy controls.
6. Configure the Windows 11 VM to use the domain controller for DNS.
7. Join `WIN11-CLIENT` to `lab.local`.
8. Validate DNS resolution and domain authentication.

## Validation evidence

| Validation | Expected outcome | Evidence |
|---|---|---|
| AD DS installation | Domain Services role installed | [Screenshot](../screenshots/server-manager-ad-ds.png) |
| OU design | Users, computers, and admins separated | [Screenshot](../screenshots/aduc-ou-structure.png) |
| Password policy | Domain policy is enforced | [Screenshot](../screenshots/password-policy-enforcement.png) |
| Client DNS | Client resolves domain resources through DC01 | [Screenshot](../screenshots/client-dns-resolution-nslookup.png) |
| Domain membership | WIN11-CLIENT authenticates as a domain user | [Screenshot](../screenshots/client-domain-authentication-whoami.png) |

## Security relevance

Active Directory is an organization’s identity control plane. The completed lab demonstrates the baseline administration and troubleshooting needed before monitoring authentication, account creation, group membership, and privileged activity in a SIEM.

## Current scope

**Completed:** AD DS, DNS, OU design, password policy, Windows client domain join, and validation.  
**Not yet implemented:** Windows event forwarding, SIEM ingestion, alerting, and detections.

No production identities, credentials, or organizational data are included.
