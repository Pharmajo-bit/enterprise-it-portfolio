# Domain Password and Account Lockout Policy

## Summary

Strengthened domain authentication by configuring password requirements and account lockout protection through Group Policy, then tested lockout and administrative recovery on a domain-joined client.

| Item | Details |
|---|---|
| Server | Windows Server 2022 |
| Client | Domain-joined Windows 11 |
| Domain | `lab.local` |
| Policy | Default Domain Policy |
| Tools | GPMC and Active Directory Users and Computers |

## Security requirements

| Control | Setting |
|---|---|
| Minimum password length | 12 characters |
| Password complexity | Enabled |
| Maximum password age | 90 days |
| Lockout threshold | 5 failed attempts |
| Lockout duration | 15 minutes |
| Reset counter after | 15 minutes |

## Business requirement

The domain needed consistent password controls and protection against repeated password guessing. Settings had to be centrally enforced for domain users and recoverable by an administrator when a legitimate account became locked.

## Implementation

### 1. Review the existing policy

Reviewed the Default Domain Policy to establish the current authentication baseline.

![Existing policy review](figure1.png)

### 2. Configure password requirements

Enabled complexity, a 12-character minimum and a 90-day maximum password age under Account Policies.

![Password policy](figure2.png)

### 3. Configure account lockout

Set the domain to lock an account after five invalid sign-in attempts for 15 minutes and reset the counter after 15 minutes.

![Account lockout policy](figure3.png)

### 4. Deploy the policy

Refreshed Group Policy on the domain controller and client:

```powershell
gpupdate /force
```

![Policy deployment](figure4.png)

## Functional testing

A test user entered an incorrect password five times. The account became locked and authentication was denied. The account was then unlocked in Active Directory Users and Computers and successfully used to sign in with the correct password.

| Test | Expected | Result |
|---|---|---|
| Five failed sign-ins | Account locked | Pass |
| Sign-in while locked | Access denied | Pass |
| Administrator unlocks account | Account restored | Pass |
| Correct password after recovery | Sign-in succeeds | Pass |

![Account lockout confirmed](figure5.png)

![Administrative account recovery](figure6.png)

## Outcome

The domain now centrally enforces the defined password and lockout controls. Testing verified both the security response and the support recovery procedure, reflecting a common identity-administration task.

## Skills demonstrated

Password policy · Account lockout · Group Policy · Active Directory · Authentication security · Account recovery · Windows Server 2022 · Functional testing

[Back to Windows Server projects](../)
