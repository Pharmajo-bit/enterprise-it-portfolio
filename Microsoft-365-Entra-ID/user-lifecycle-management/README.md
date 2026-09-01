# Microsoft Entra ID User Lifecycle Management

## Summary

Managed a fictional employee through onboarding, a department transfer and secure offboarding in Microsoft Entra ID and Microsoft 365. The project covers identity attributes, group-based access, Exchange Online resources, licensing and audit validation.

| Item | Details |
|---|---|
| Organisation | Abdalla Technologies |
| User | Ahmed Ali |
| Initial department | Finance |
| New department | Human Resources |
| Platforms | Microsoft Entra ID, Microsoft 365 and Exchange Online |
| Control model | Group-based access and lifecycle administration |

## Business requirement

Ahmed required a cloud identity, licence, reporting relationship and department access when joining Finance. After transferring to HR, his identity and access needed to reflect the new role without retaining unnecessary Finance access. When he left the organisation, sign-in had to be blocked, licensing reclaimed and the administrative activity verified.

## Lifecycle implementation

### 1. Onboarding

Created Ahmed's account with the required user principal name, job title and Finance department attributes, then assigned Fatima Noor as his manager.

![Initial user profile](picture1.png)

![Manager assignment](Picture2.png)

### 2. Department transfer

Removed the previous Finance group assignment, added Ahmed to the HR security group, and updated his department and job title.

![Group membership updated](Picture3.png)

![Department and title updated](Picture4.png)

This change aligns access with the current role and avoids leaving permissions behind after an internal transfer.

### 3. Collaboration access

Granted Ahmed access to the HR shared mailbox and added him to the HR distribution list.

![HR shared mailbox access](Picture5.png)

![HR distribution list membership](Picture6.png)

### 4. Offboarding

Blocked sign-in to revoke access immediately, then removed the Microsoft 365 licence so it could be reassigned.

![Sign-in blocked](Picture7.png)

![Licence removed](Picture8.png)

### 5. Audit validation

Reviewed Microsoft Entra ID audit logs to confirm that lifecycle changes were recorded for accountability, troubleshooting and compliance.

![Audit log review](Picture9.png)

## Validation

| Lifecycle control | Result |
|---|---|
| Identity and organisational attributes created | Pass |
| Manager relationship assigned | Pass |
| Finance access removed during transfer | Pass |
| HR access and collaboration resources assigned | Pass |
| Sign-in blocked during offboarding | Pass |
| Microsoft 365 licence reclaimed | Pass |
| Administrative changes recorded in audit logs | Pass |

## Outcome

The complete joiner-mover-leaver process was implemented successfully. The project demonstrates how identity data, access, collaboration services and licensing should change with an employee's role rather than remaining static throughout employment.

## Skills demonstrated

Microsoft Entra ID · Microsoft 365 administration · Exchange Online · Joiner-mover-leaver lifecycle · Security groups · Shared mailboxes · Distribution lists · Licensing · Offboarding · Audit logs

[Back to Microsoft Entra ID projects](../)
