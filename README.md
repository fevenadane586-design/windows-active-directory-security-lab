# Windows Active Directory Security Lab

A hands-on Windows enterprise lab built in VMware to demonstrate centralized identity management, network services, Windows deployment, and access-control security using Windows Server 2022.

## Project Overview

This project documents the design and configuration of a virtual Windows domain environment. The lab combines Active Directory Domain Services (AD DS), DHCP, Windows Deployment Services (WDS), domain-joined Windows clients, user and group administration, and NTFS access controls.

The objective was not only to configure the services, but also to test whether the implemented security controls worked as intended.

## Lab Environment

| Component | Configuration |
|---|---|
| Virtualization | VMware Workstation |
| Server OS | Windows Server 2022 |
| Client OS | Windows 10 |
| Domain Controller | DC01 |
| Domain | iatek.ca |
| Directory Service | Active Directory Domain Services |
| Network Services | DNS, DHCP |
| Deployment Service | Windows Deployment Services (WDS) |

## Lab Architecture

The environment was built around a Windows Server 2022 Domain Controller running AD DS and supporting network services.

```text
                    ┌──────────────────────┐
                    │   Windows Server     │
                    │        DC01          │
                    │                      │
                    │  AD DS / DNS / DHCP  │
                    │         WDS          │
                    └──────────┬───────────┘
                               │
                         iatek.ca Domain
                               │
                ┌──────────────┴──────────────┐
                │                             │
        ┌───────▼────────┐            ┌───────▼────────┐
        │ Windows Client │            │ Windows Client │
        │      PC01      │            │      PC02      │
        └────────────────┘            └────────────────┘
```

## Part 1 — Active Directory Domain Controller

The first stage of the project established the Windows domain infrastructure.

Tasks completed included:

- Created a Windows Server 2022 virtual machine in VMware
- Configured the server as `DC01`
- Assigned a static IPv4 configuration
- Installed the Active Directory Domain Services role
- Created a new Active Directory forest
- Configured the `iatek.ca` domain
- Promoted the server to a Domain Controller
- Verified the Active Directory environment after promotion

This provided the centralized identity infrastructure used throughout the remaining stages of the lab.

## Part 2 — DHCP and Windows Deployment Services

The second stage expanded the domain environment with centralized network configuration and operating-system deployment.

### DHCP

Configured DHCP services to provide network configuration to client systems.

Tasks included:

- Installed the DHCP Server role
- Authorized the DHCP server in Active Directory
- Created and configured a DHCP scope
- Defined address exclusions
- Configured lease settings
- Verified DHCP operation

### Windows Deployment Services

Windows Deployment Services was configured to support network-based Windows installation.

Tasks included:

- Installed the WDS role
- Integrated WDS with Active Directory
- Configured boot and installation images
- Configured PXE-based deployment
- Booted a client through the network
- Successfully deployed Windows 10 through WDS

## Part 3 — Identity and Access Security

The final stage focused on user administration and access-control security within the domain.

### Organizational Structure

Created and managed:

- Organizational Units (OUs)
- Domain user accounts
- Security groups
- Group memberships

This allowed permissions and restrictions to be managed through centralized identities rather than individual local accounts.

### Account Restrictions

Several account-level controls were configured and tested, including:

- Login-hour restrictions
- Workstation login restrictions
- Account expiration
- Account disablement

A restricted account was tested against an unauthorized workstation to verify that the login restriction was enforced.

### NTFS Permissions and Shared Resources

Shared folders were configured with NTFS permissions to demonstrate role-based access.

The lab included:

- Security-group-based permissions
- Permission inheritance
- Shared folder access
- Restricted folder access
- Least-privilege permission testing

Access testing confirmed that an authorized user could access the permitted resource while being denied access to a folder outside the user's assigned permissions.

## Security Controls Demonstrated

This lab demonstrates several foundational enterprise security concepts:

- Centralized authentication through Active Directory
- Role-based access using security groups
- Least-privilege access control
- Account lifecycle management
- Login-hour restrictions
- Workstation-based login restrictions
- NTFS file and folder permissions
- Permission inheritance
- Centralized network configuration
- Controlled Windows client deployment

## Testing and Validation

Configuration alone does not demonstrate that a security control works. For this reason, several controls were validated after implementation.

Examples included:

- Confirming successful Domain Controller promotion
- Verifying DHCP configuration
- Testing PXE-based Windows deployment
- Joining Windows clients to the domain
- Testing workstation login restrictions
- Testing authorized and unauthorized folder access
- Confirming NTFS permission enforcement

## Skills Demonstrated

- Windows Server 2022 administration
- Active Directory Domain Services
- Domain Controller configuration
- DNS and DHCP administration
- Windows Deployment Services
- User and group administration
- Organizational Unit management
- Domain joining
- Identity and access management
- NTFS permissions
- Least-privilege security
- VMware virtualization
- Security control testing and validation

## Project Documentation

Detailed documentation and screenshots will be organized into the following sections:

```text
docs/
├── 01-domain-controller-setup.md
├── 02-dhcp-wds-deployment.md
└── 03-identity-access-security.md

screenshots/
├── active-directory/
├── dhcp-wds/
└── access-control/
```

## Key Takeaway

This project demonstrates how Active Directory can be used as the foundation for centralized identity, network administration, system deployment, and access control in a Windows domain environment.

Rather than only configuring services, the lab also included validation of security restrictions and permissions to confirm that the implemented controls behaved as intended.

## Author

**Feben Adane**

Cybersecurity trainee interested in SOC operations, Windows security, identity and access management, network security, and threat detection.
