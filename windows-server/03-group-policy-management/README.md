# Targeted Group Policy Management

## Summary

Created and deployed a Group Policy Object that blocked HR users from opening Control Panel and Windows Settings without affecting other departments.

| Item | Details |
|---|---|
| Server | Windows Server 2022 |
| Client | Domain-joined Windows 11 |
| Domain | `lab.local` |
| Tool | Group Policy Management Console |
| Target | `CorpUsers\HR` OU |
| GPO | `HR - Block Control Panel` |

## Business requirement

Unauthorised workstation changes by HR users were creating inconsistent configurations and additional support work. The restriction needed to target HR only, leaving IT and Finance unaffected.

## Implementation

### 1. Prepare the OU structure

Organised users beneath departmental OUs and placed the HR account in the HR OU to provide a precise policy target.

![Departmental OU structure](figure1.png)

### 2. Create and configure the GPO

Created `HR - Block Control Panel` and enabled:

> User Configuration → Policies → Administrative Templates → Control Panel → Prohibit access to Control Panel and PC settings

![GPO created](figure2.png)

![Control Panel restriction enabled](figure3.png)

### 3. Link the policy to HR

Linked the GPO to the HR OU so the restriction applied to HR users rather than the entire domain.

![GPO linked to HR OU](figure4.png)

### 4. Apply and verify the policy

Forced a policy refresh and reviewed the resultant policy:

```powershell
gpupdate /force
gpresult /r
```

`gpresult` confirmed that the HR restriction was applied to the intended user.

![Policy refresh and resultant policy](figure5.png)

## Functional testing

| Test | Expected | Result |
|---|---|---|
| HR user opens Control Panel | Access denied | Pass |
| HR user opens Windows Settings | Access denied | Pass |
| `gpresult /r` lists the HR GPO | GPO present | Pass |
| Policy remains scoped to HR OU | Other departments unaffected | Pass |

![Control Panel blocked for HR user](figure6.png)

## Outcome

The targeted restriction was successfully deployed and verified on the Windows 11 client. The project demonstrates OU-based scoping, centralised endpoint control and the use of native tools to validate actual policy application.

## Skills demonstrated

Group Policy · Active Directory OUs · GPMC · `gpupdate` · `gpresult` · Targeted policy deployment · Windows endpoint administration · Functional testing

[Back to Windows Server projects](../)
