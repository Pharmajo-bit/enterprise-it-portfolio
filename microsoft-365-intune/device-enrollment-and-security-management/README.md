# Windows Endpoint Management and Security with Microsoft Intune

## Summary

Enrolled a Windows 11 device into Microsoft Intune, targeted it through a Microsoft Entra security group, deployed configuration and security policies, installed Google Chrome as a Win32 application, and configured Conditional Access for privileged roles.

| Item | Details |
|---|---|
| Device | `PRACTICELAB` |
| Operating system | Windows 11 |
| Identity | Microsoft Entra ID |
| Management | Microsoft Intune MDM |
| Endpoint protection | Microsoft Defender Antivirus |
| Application | Google Chrome Win32 package |
| Identity control | MFA for administrative roles |

## Business requirement

Abdalla Technologies required a controlled test environment for centralised Windows endpoint administration. The device needed consistent configuration, compliance evaluation, endpoint protection, automated software deployment and stronger authentication for administrators.

## Implementation and evidence

### 1. Create device groups

Created Test, Shared, IT, HR and Finance device groups in Microsoft Entra ID to support scalable, group-based assignments.

![Microsoft Entra device groups](images/Picture1.png)

### 2. Enrol and target the Windows device

Connected `PRACTICELAB` to the tenant, enrolled it into Intune MDM and added it to the Test Devices group.

![Device enrolled in Intune](images/Picture2.png)

![Device assigned to Test Devices](images/Picture3.png)

### 3. Deploy a configuration baseline

Created and assigned the **Corporate Security Baseline** configuration profile to Test Devices.

![Configuration profile](images/Picture4.png)

### 4. Evaluate device compliance

Created the **Corporate Windows Compliance Policy**, configured the organisation's security requirements and assigned it to Test Devices.

![Compliance policy](images/Picture5.png)

![Compliance requirements](images/Picture6.png)

![Compliance assignment](images/Picture7.png)

### 5. Configure endpoint protection

Created a Microsoft Defender Antivirus endpoint-security policy and targeted it to Test Devices.

![Defender Antivirus policy](images/Picture8.png)

![Defender configuration and assignment](images/Picture9.png)

![Defender policy created](images/Picture10.png)

### 6. Deploy a Win32 application

Packaged Google Chrome with installation and detection rules, assigned it to Test Devices and confirmed successful installation.

![Chrome Win32 configuration](images/Picture11.png)

![Chrome assignment](images/Picture12.png)

![Successful Chrome deployment](images/Picture13.png)

### 7. Protect privileged identities

Created **Require MFA for Administrative Roles** in Conditional Access. The policy targeted administrative directory roles, excluded emergency-access accounts and required MFA for Microsoft cloud applications.

![Conditional Access policy](images/Picture14.png)

![Administrative roles targeted](images/Picture15.png)

![MFA grant control](images/Picture16.png)

![Completed Conditional Access policy](images/Picture17.png)

## Validation

| Control | Result |
|---|---|
| Windows device enrolled and visible in Intune | Pass |
| Device targeted through Test Devices group | Pass |
| Configuration profile assigned | Pass |
| Compliance policy configured and assigned | Pass |
| Defender Antivirus policy assigned | Pass |
| Chrome reported as successfully installed | Pass |
| Administrative-role MFA policy configured | Pass |

## Outcome

The device was brought under central management and received configuration, compliance, endpoint-security and application controls through group-based assignments. Conditional Access added identity protection for privileged roles, demonstrating how device and identity controls work together in Microsoft 365.

## Skills demonstrated

Microsoft Intune · Windows enrollment · Microsoft Entra ID · Device groups · Configuration profiles · Compliance policies · Defender Antivirus · Win32 deployment · Conditional Access · MFA · Policy validation

[Back to Microsoft Intune projects](../)
