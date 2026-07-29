# Case Study 02 – Secure Department File Share (NTFS Permissions & Access Control)

**Category:** Windows Server Administration

**Technology Stack:** Windows Server 2022 | Active Directory Domain Services | Windows 11 | VMware Workstation

**Author:** Abdalla Hussein

**Status:** Completed

**Last Updated:** July 2026

---

## Overview

This case study demonstrates the implementation of a secure departmental file share within a Windows Server 2022 environment using Active Directory security groups, SMB file sharing, and NTFS permissions.

The objective was to provide authorized Human Resources (HR) personnel with secure access to departmental resources while preventing unauthorized access through Role-Based Access Control (RBAC).

A dedicated HR shared folder and subfolder were created and configured using both Share Permissions and NTFS Permissions. Access was assigned through the existing HR security group rather than individual user accounts, ensuring centralized permission management and adherence to the principle of least privilege.

The completed configuration was validated to confirm that the required security and access control requirements were successfully implemented.

This project demonstrates core Windows Server administration skills commonly used to secure enterprise file servers and manage access to sensitive business data.

---

## Business Scenario

The Human Resources department requires a secure network location to store employee records and other confidential documentation. Due to the sensitive nature of this information, access must be restricted to authorized HR personnel while preventing access by users from other departments.

As the Systems Administrator, the objective is to implement a secure departmental file share using Active Directory security groups, SMB file sharing, and NTFS permissions.

Access is assigned through the existing HR security group rather than individual user accounts, ensuring a scalable and centrally managed permission model that aligns with the principles of Role-Based Access Control (RBAC) and least privilege.

---

## Environment

| Component | Configuration |
|-----------|---------------|
| Hypervisor | VMware Workstation |
| Domain Controller | Windows Server 2022 |
| Client Device | Windows 11 |
| Domain | lab.local |
| Shared Folder | C:\Shares\HR |
| Security Group | HR |

---

# Implementation

## Folder Structure Created

A dedicated directory structure was created to store Human Resources data.

The shared folder was organized to separate departmental information from employee-specific records, providing a structured foundation for secure file storage.

The following directory structure was created:

- `C:\Shares\HR`
- `C:\Shares\HR\Employee Records`

A sample document named **salary-review.txt** was added to simulate confidential business data for access validation.

![Figure 1](figure1.png)

**Figure 1.** Human Resources folder structure created on the Windows Server.

---

## Network Share Configured

The Human Resources folder was configured as an SMB network share to allow authorized users to access departmental resources across the network.

The share was created using the name **HRShare**, providing a centralized location for HR personnel to securely store and retrieve files.

Creating the folder as a network share enables users to access the resource from domain-joined devices without requiring direct access to the server's local file system.

![Figure 2](figure2.png)

**Figure 2.** SMB network share configured for the Human Resources department.

---

## Share Permissions Configured

Share permissions were configured to ensure that only authorized Human Resources personnel could access the network share.

Broad access permissions were removed, and access was assigned to the HR security group to support centralized permission management.

Members of the HR security group were granted **Read** and **Change** permissions, allowing them to:

- View files
- Create files
- Modify files
- Delete files

while preventing unauthorized users from accessing the network share.

![Figure 3](figure3.png)

**Figure 3.** Share permissions configured for the HR network share.

---

## NTFS Permissions Configured

NTFS permissions were configured on the Human Resources shared folder to provide file system-level access control.

Administrative permissions for **SYSTEM** and **Administrators** were retained to ensure ongoing management and system functionality, while the HR security group was granted **Modify** permissions.

Unnecessary inherited permissions were removed where appropriate to restrict access and ensure that only authorized HR personnel could access and modify the folder contents.

This layered permission model provides an additional level of security beyond Share Permissions and helps protect sensitive organizational data.

![Figure 4](figure4.png)

**Figure 4.** NTFS permissions configured for the HR shared folder.

---

# Security Model

## Role-Based Access Control (RBAC) Implemented

Access to the Human Resources file share was managed through the existing HR Active Directory security group rather than by assigning permissions directly to individual user accounts.

This implementation follows the principles of Role-Based Access Control (RBAC), where permissions are assigned to security groups and users inherit access through group membership.

By centralizing access management through Active Directory security groups:

- User onboarding becomes easier.
- Role changes require minimal administration.
- Offboarding can be completed without modifying folder permissions.
- Administrative overhead is reduced.
- Security remains consistent across the environment.

This approach provides a scalable permission model suitable for enterprise environments.

---

# Validation

The completed configuration was verified to ensure the network share, Share Permissions, NTFS Permissions, and Active Directory security group were correctly configured.

| Validation Check | Result |
|------------------|--------|
| HR network share successfully created | ✅ Passed |
| Folder structure created successfully | ✅ Passed |
| Share permissions assigned to the HR security group | ✅ Passed |
| NTFS permissions configured correctly | ✅ Passed |
| Administrative access retained | ✅ Passed |
| Access model aligned with business requirements | ✅ Passed |

---

# Outcome

The secure Human Resources file share was successfully implemented using SMB file sharing, NTFS permissions, and Active Directory security groups.

Access to departmental resources was centrally managed through the HR security group, ensuring that only authorized users could access sensitive information while maintaining administrative control.

The completed implementation demonstrates a layered security approach commonly used to protect enterprise file servers.

---

# Key Takeaways

- Share Permissions and NTFS Permissions work together to determine effective access to shared resources.
- Active Directory security groups provide a scalable and centralized method of managing file access.
- Implementing Role-Based Access Control (RBAC) simplifies permission management and reduces administrative effort.
- Applying the principle of least privilege helps protect sensitive organizational data while maintaining operational efficiency.

---

# Skills Demonstrated

## Windows Server Administration

- SMB file sharing
- NTFS permission management
- Shared folder administration

## Identity & Access Management

- Active Directory security groups
- Role-Based Access Control (RBAC)
- Permission delegation

## Enterprise Security

- Share Permissions
- NTFS Permissions
- Principle of least privilege
- Layered access control

## Documentation & Validation

- Technical documentation
- Configuration validation
- Enterprise implementation practices
