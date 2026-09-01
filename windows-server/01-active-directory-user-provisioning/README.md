# Active Directory User Provisioning and RBAC

## Summary

Provisioned a new Human Resources employee in Active Directory, assigned access through a departmental security group, and verified the completed identity configuration from a domain-joined Windows 11 client.

| Item | Details |
|---|---|
| Platform | Windows Server 2022 and Windows 11 |
| Directory | Active Directory Domain Services |
| Domain | `lab.local` |
| User | Sarah Ahmed (`sahmed`) |
| Access model | Role-Based Access Control through the HR security group |
| Virtualisation | VMware |

## Business requirement

A new HR employee required a domain account and department-based access. Permissions needed to be administered through a security group rather than assigned directly to the user, providing a scalable and consistent access model.

## Implementation

### 1. Create the user account

Created Sarah Ahmed's account using the organisation's naming convention and required a password change at first sign-in.

![Sarah Ahmed user account](figure1.png)

![Initial password settings](figure2.png)

### 2. Create the departmental security group

Created a global security group for Human Resources so department permissions could be managed centrally.

![HR security group](figure3.png)

### 3. Assign role-based access

Added Sarah's account to the HR security group. This allows access to follow group membership instead of relying on direct user permissions.

![HR group membership](figure4.png)

## Validation

| Check | Result |
|---|---|
| User account created and enabled | Pass |
| HR security group created | Pass |
| User added to the correct group | Pass |
| Membership visible from the provisioned account | Pass |

![Provisioned account validation](figure5.png)

## Outcome

The employee account was successfully provisioned with department-based access. The implementation demonstrates a repeatable onboarding approach using Active Directory users, security groups and RBAC.

## Skills demonstrated

Active Directory administration · User provisioning · Security groups · RBAC · Least privilege · Windows Server 2022 · Configuration validation

[Back to Windows Server projects](../)
