# Windows Server Administration

This section contains hands-on Windows Server 2022 projects completed in an Active Directory lab with a domain-joined Windows 11 client.

The projects follow a connected business environment: identities are provisioned through Active Directory, access is assigned through security groups, departmental data is protected with file permissions, and domain security settings are centrally enforced through Group Policy.

## Environment

| Component | Details |
|---|---|
| Server | Windows Server 2022 |
| Client | Windows 11, domain joined |
| Directory | Active Directory Domain Services |
| Domain | `lab.local` |
| Virtualisation | VMware |
| Administration | ADUC, GPMC, SMB and NTFS permissions |

## Projects

| Case study | Practical evidence |
|---|---|
| [01 – Active Directory user provisioning and RBAC](01-active-directory-user-provisioning/) | Created a departmental user and security group, assigned group membership and validated the resulting identity configuration. |
| [02 – Secure departmental file share](02-secure-department-file-share/) | Configured an SMB share with group-based share and NTFS permissions, then tested authorised and unauthorised access. |
| [03 – Group Policy management](03-group-policy-management/) | Created, linked and validated a user policy in the domain environment using a Windows 11 client. |
| [04 – Domain password and account lockout policy](04-password-policy-management/) | Enforced domain password requirements and account lockout controls, tested failed sign-ins and verified administrative recovery. |

## Skills demonstrated

- Active Directory Domain Services
- User and security-group administration
- Role-Based Access Control
- Group Policy Management
- SMB file sharing
- NTFS and share permissions
- Password and account lockout policies
- Windows 11 domain administration
- Functional access testing
- Technical documentation

[Return to the portfolio homepage](../)
