# ServiceNow Service Desk Lab

## Overview

I recreated the strongest parts of my osTicket operating model in a ServiceNow Personal Developer Instance. The lab focuses on the controls and workflows commonly used by enterprise support teams: assignment groups, group-based access, incident ownership, L1/L2 escalation, SLAs, knowledge management and operational reporting.

The purpose was not to duplicate every osTicket scenario. It was to demonstrate that the same IT service-management practices can be transferred into ServiceNow and validated through realistic ticket lifecycles.

> **Lab scope:** All users, incidents and technical actions are fictional and were created in a personal developer instance. Work notes identify simulated investigation and remediation steps. No production system, corporate account or genuine user data was involved.

## What I implemented

- Created Service Desk, Infrastructure Support and Security Operations assignment groups.
- Created representative support analysts and business users.
- Granted the standard `itil` role through group membership rather than directly to individuals.
- Validated inherited access by impersonating an L1 analyst.
- Configured a one-hour Critical Incident Response SLA with start and stop conditions.
- Completed four incidents covering Critical, High, Moderate and Low priorities.
- Documented L1 resolution, L1-to-L2 escalation, technical handback and customer-facing closure.
- Published an Outlook credential troubleshooting knowledge article.
- Created an incident-priority report and an operational dashboard.

## Assignment groups and group-based access

I created three assignment groups to separate operational responsibility:

| Group | Responsibility | Representative analyst |
|---|---|---|
| Service Desk | Intake, triage, user communication and standard L1 resolution | Alex Morgan |
| Infrastructure Support | Servers, networks, applications and escalated technical incidents | Daniel Kim |
| Security Operations | Suspected compromise and security-incident investigation | Sarah Chen |

![ServiceNow assignment groups](images/01-assignment-groups.png)

Six active accounts represent three support analysts and three business users. The business users received no support role or assignment-group membership.

![Support and requester accounts](images/02-support-and-requester-accounts.png)

The `itil` role was assigned to the support groups so members inherit access through group membership. Impersonating Alex Morgan confirmed that an L1 analyst could access the Incident modules without administrator privileges.

![Group-inherited ITIL access](images/03-group-inherited-itil-access.png)

![Impersonation validation](images/04-impersonation-validation.png)

## SLA configuration

I created an active **Critical Incident Response SLA - 1 Hour** for Priority 1 incidents. The SLA starts when a matching incident is active and stops when the incident reaches Resolved or Closed.

![Critical incident SLA definition](images/05-critical-incident-sla.png)

ServiceNow attached the custom SLA to the warehouse printing incident and tracked elapsed time, remaining time and progress alongside the platform's existing SLA.

![SLA applied to the critical incident](images/06-sla-applied-to-incident.png)

## Incident workflows

### 1. Outlook credential loop — L1 resolution

The caller could access Microsoft 365 webmail after a password change, but Outlook repeatedly requested credentials. This isolated the problem to the desktop client rather than the account or mailbox.

The controlled L1 workflow documented removal of stale Microsoft 365 credentials from Windows Credential Manager, an Outlook restart, sign-in with the updated password and successful mailbox synchronisation.

![Outlook incident created](images/07-outlook-incident-created.png)

![Resolved Outlook incident](images/08-outlook-l1-resolution.png)

### 2. Finance shared-drive access — identity and access troubleshooting

The shared-drive incident documented verification of the user's department and access requirement, correction of the assumed Active Directory group membership, a Windows security-token refresh and confirmation that the required share was available.

This scenario connects the ServiceNow workflow to the Active Directory and secure file-share projects elsewhere in this portfolio.

![Resolved shared-drive incident](images/09-shared-drive-resolution.png)

### 3. Payroll application outage — L1-to-L2 escalation

Service Desk confirmed that multiple Payroll users were affected while Microsoft 365 remained available, recorded the business impact and escalated the application outage to Infrastructure Support rather than performing an unauthorised service restart.

![L1 payroll triage and escalation](images/10-payroll-l1-escalation.png)

Infrastructure documented the simulated application-service investigation and recovery, then returned ownership to Service Desk for user communication and closure.

![Infrastructure handback to Service Desk](images/11-payroll-l2-handback.png)

![Resolved payroll incident](images/12-payroll-resolution.png)

### 4. Critical warehouse printing incident — SLA breach and corrective workflow

The warehouse incident represented four packing stations unable to print shipping labels. It was assigned Priority 1 - Critical and deliberately left unresolved in this controlled exercise to validate SLA breach detection.

ServiceNow recorded zero business time remaining and displayed the breached SLA in red.

![SLA breach evidence](images/13-sla-breach-evidence.png)

Service Desk acknowledged the controlled breach, documented the business risk and escalated the simulated print-service investigation to Infrastructure Support.

![SLA breach escalation](images/14-sla-breach-escalation.png)

Infrastructure modelled clearing a blocked print queue and restarting the Print Spooler, then returned the incident to Service Desk.

![Infrastructure remediation and handback](images/15-infrastructure-handback.png)

The final record preserved the breached SLA outcome while documenting customer communication, corrective review and resolution.

![SLA corrective closure](images/16-sla-corrective-closure.png)

## Knowledge management

I converted the Outlook resolution into a published ServiceNow knowledge article. It records the symptoms, likely cause, repeatable resolution procedure and specific escalation conditions, including account lockout, Conditional Access failure and suspected compromise.

![Published Outlook troubleshooting article](images/17-published-knowledge-article.png)

## Reporting and dashboard

I created a filtered report using the four lab incidents and grouped the results by priority. This produced one resolved incident at each priority level and excluded ServiceNow demo records.

![Resolved lab incidents by priority](images/18-priority-report.png)

The report was recreated as a Platform Analytics data visualisation and added to a ServiceNow Service Desk Lab dashboard.

![ServiceNow Service Desk Lab dashboard](images/19-service-desk-dashboard.png)

## Skills demonstrated

- ServiceNow incident, knowledge and service-level management
- Assignment groups and group-inherited `itil` access
- Impersonation testing and separation of administrator/analyst privileges
- Ticket categorisation, impact, urgency and priority management
- L1 troubleshooting and customer communication
- L1-to-L2 escalation, reassignment, handback and closure
- SLA attachment, breach detection and corrective review
- Knowledge-article development and escalation criteria
- Report filtering, aggregation and dashboard visualisation
- Clear separation of controlled simulation from production experience

## Comparison with osTicket

| Area | osTicket | ServiceNow |
|---|---|---|
| Access model | Departments, teams and custom roles | Assignment groups and inherited platform roles |
| Ticket record | Lightweight ticket threads and internal notes | Structured incidents, states, work notes, comments and related records |
| SLA evidence | Due date and overdue event | Task SLA records, elapsed percentage and retained breach status |
| Knowledge | Built-in FAQ/knowledge content | Versioned knowledge workflow and published article portal |
| Reporting | Operational queues and filters | Reports, data visualisations and Platform Analytics dashboards |

## Outcome

This project demonstrates that I can apply consistent ITSM practices across both a lightweight open-source platform and an enterprise service-management platform. The completed workflows show technical troubleshooting, ownership boundaries, escalation discipline, SLA awareness, reusable documentation and operational reporting.
