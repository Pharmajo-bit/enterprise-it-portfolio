# osTicket Service Desk Operations Lab

## Overview

I deployed and configured an osTicket service desk in Docker Desktop, then used it to document realistic support operations across identity, Microsoft 365, endpoint, network and infrastructure scenarios.

The goal was not simply to install a ticketing system. I wanted to demonstrate how an L1/L2 support team records incidents, applies least privilege, works to SLAs, escalates by technical responsibility, validates outcomes and converts repeat fixes into reusable knowledge.

> **Lab scope:** This is a personal homelab using fictional users and business scenarios. Technical workflows aligned to my Windows Server, Microsoft Entra ID and Intune labs are identified below. The payroll, security-response and SLA-breach exercises are explicitly documented as simulations; no production system or genuine user data was involved.

## Environment

- Windows 11 Home host
- Docker Desktop
- osTicket container: `rinkp/osticket-dockerized:main-patches`
- MariaDB 10.11
- Docker network: `service-desk-network`
- Web application: port `8080`

## What I implemented

- Deployed osTicket with a separate MariaDB container.
- Added the required application secret and administrator environment variables.
- Configured Service Desk, Infrastructure and Security departments.
- Created representative L1/L2 agents and responsibility boundaries.
- Applied role-based access control and withheld destructive permissions from Service Desk analysts.
- Configured standard and critical-incident SLA plans.
- Created help topics, canned responses and internal knowledge content.
- Documented ticket assignment, internal notes, escalation, handback, validation and closure.

![Healthy osTicket and MariaDB containers](images/01-healthy-containers.png)

## Troubleshooting the deployment

The osTicket web application installed successfully, but Docker continued reporting the container as unhealthy. I inspected the container health output and found that the image's default health check called `curl`, which was not installed in the container.

I replaced the failing check with an executable `wget` request to `http://localhost`. After recreating the container, the health status changed to healthy while the application remained accessible on port 8080.

This separated application availability from health-check implementation: the service itself was working, but Docker was testing it with an unavailable utility.

## Service desk structure and access control

I created three operational departments and assigned a representative agent to each:

| Agent | Department | Responsibility |
|---|---|---|
| Alex Morgan | Service Desk | Initial triage, user communication and common L1 resolution |
| Daniel Kim | Infrastructure | Privileged infrastructure and application-service work |
| Sarah Chen | Security | Security assessment and incident-response procedures |

![Configured service desk agents](images/02-agents-and-departments.png)

![Configured departments](images/03-departments.png)

The Service Desk Analyst role can assign, close, edit, reply, refer, release and transfer tickets. Delete access, cross-agent thread editing and other destructive capabilities were withheld to demonstrate least privilege and separation of duties.

![Least-privilege Service Desk permissions](images/04-service-desk-rbac.png)

## Operational workflows

### 1. Department transfer and shared-drive access

A user moved from Finance to HR but retained the old group membership and could not access the HR share. The workflow documented verification of the access model, removal from `Finance_Users`, addition to `HR_Users`, Windows security-token refresh and confirmation that the new access worked while the old access was removed.

This scenario aligns with the Active Directory group and secure file-share work elsewhere in this portfolio.

![Resolved HR shared-drive access ticket](images/05-hr-shared-drive-resolution.png)

### 2. Intermittent endpoint connectivity

The affected laptop had assigned itself an APIPA address and had no default gateway. Other clients were receiving DHCP leases, which isolated the fault to the endpoint rather than the DHCP server or scope. The documented resolution reset the wireless adapter, renewed the lease and validated internet and shared-drive access.

![Resolved APIPA and DHCP ticket](images/06-apipa-dhcp-resolution.png)

### 3. Outlook credential loop

Successful Outlook on the web access established that the Microsoft 365 account and mailbox were operational. The investigation then focused on the desktop client, where an outdated Microsoft 365 entry in Windows Credential Manager was identified and removed. Exchange connectivity and mail synchronisation were validated before closure.

![Resolved Outlook credential ticket](images/07-outlook-credential-resolution.png)

### 4. L1-to-L2 payroll outage escalation

In this simulated multi-user outage, Service Desk reproduced an HTTP 503 error, confirmed that other business services remained available, assessed the business impact and escalated the application-service fault to Infrastructure rather than attempting an unauthorised production restart.

![Service Desk impact assessment and escalation](images/08-payroll-l1-escalation.png)

Infrastructure documented the assumed failed overnight update, modelled rollback and service restoration, then returned ownership to Service Desk for user validation and closure.

![Infrastructure remediation and Service Desk handback](images/09-payroll-l2-resolution.png)

### 5. OneDrive performance degradation

Task Manager analysis identified OneDrive consuming more than 4 GB of memory while repeatedly processing a large project folder. The workflow documented pausing synchronisation, moving temporary application data outside the synchronised location, resuming OneDrive and monitoring system responsiveness.

![Resolved OneDrive performance ticket](images/10-onedrive-performance-resolution.png)

### 6. New-starter onboarding

The onboarding request brings together my related AD, Microsoft 365 and Intune lab work: account creation, temporary-password controls, group-based Finance access, Microsoft 365 licensing, Windows enrollment, compliance, MFA and application provisioning. It also records troubleshooting an incorrect ARM64 application requirement on an x64 endpoint.

![Completed Finance onboarding workflow](images/11-finance-onboarding.png)

### 7. Security-response handoff

This controlled exercise modelled how Service Desk should escalate an unexpected MFA prompt and suspected account compromise without exceeding its authority. Security documented the production containment procedure, and the ticket clearly states that no genuine security incident or corporate account was involved.

![Transparent security-response simulation](images/12-security-response-simulation.png)

## Knowledge management

I converted the Outlook credential-loop resolution into an internal knowledge-base article. The article records symptoms, likely cause, a repeatable diagnostic sequence, safety guidance and escalation conditions.

![Internal Outlook troubleshooting article](images/13-outlook-knowledge-article.png)

## SLA monitoring and corrective workflow

I created an active Critical Incident SLA with a one-hour grace period and a 24/7 schedule.

![Critical Incident SLA configuration](images/14-critical-incident-sla.png)

An Emergency-priority warehouse printing ticket was deliberately left unresolved in this controlled exercise. osTicket calculated the deadline and later created a system event marking the ticket overdue.

![System-generated overdue ticket evidence](images/15-sla-overdue-detection.png)

Service Desk acknowledged the breach, documented the control test and escalated the simulated print-service incident to Infrastructure.

![SLA breach acknowledgement and escalation](images/16-sla-breach-escalation.png)

Infrastructure modelled queue and Print Spooler recovery, returned ownership to Service Desk, and the final note recorded the breached target, successful overdue detection, escalation path and corrective workflow.

![Completed SLA corrective review](images/17-sla-corrective-review.png)

## Skills demonstrated

- Docker container deployment and health-check troubleshooting
- Ticket intake, categorisation, prioritisation and ownership
- L1 endpoint, identity and Microsoft 365 troubleshooting
- L1-to-L2 escalation and separation of duties
- RBAC and least-privilege administration
- SLA configuration, overdue monitoring and post-breach review
- Clear internal notes, user-impact summaries and closure records
- Knowledge-base development and escalation criteria
- Honest separation of implemented lab work from simulated operational exercises

## Enterprise-platform continuation

I recreated the strongest parts of this operating model in a [ServiceNow Personal Developer Instance](../servicenow-service-desk-lab/), focusing on assignment groups, group-based access, incident states, SLAs, knowledge publishing and operational reporting.
