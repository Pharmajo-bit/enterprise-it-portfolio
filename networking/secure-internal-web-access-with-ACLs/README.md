# Securing an Internal Web Service with Extended ACLs

## Summary

Protected a Finance payroll web application with an extended ACL: HR could ping the server to verify availability but could not access it over HTTP, while IT retained administrative access.

| Item | Details |
|---|---|
| Router | Cisco 2911 |
| Switch | Cisco Catalyst 2960 |
| Application | Finance HTTP server |
| Policy | `HR_WEB_POLICY` |
| Target interface | HR subinterface, inbound |
| Platform | Cisco Packet Tracer |

## Business requirement

The Finance web service needed to remain available to authorised personnel. HR required basic reachability testing but no browser access, and IT required unrestricted access for administration.

## Implementation

### 1. Deploy the service

Configured the Finance server with a static address and enabled HTTP.

![Finance server configuration](images/Screenshot-2026-08-04%20200856.png)

![HTTP service enabled](images/picture3-http-en.png)

### 2. Apply application-level filtering

Created `HR_WEB_POLICY` to permit ICMP while denying TCP port 80 from HR to the Finance server, then applied it inbound on the HR subinterface.

![Extended ACL configuration](images/show-access-lists.png)

![ACL applied to HR interface](images/acl-applied-interface.png)

## Topology and validation

![Network topology](images/picture1-network-topology.png)

| Test | Expected | Result |
|---|---|---|
| HR pings Finance server | Allowed | Pass |
| HR opens Finance website | Blocked | Pass |
| IT opens Finance website | Allowed | Pass |

![HR reachability test](images/hr-ping-server.png)

![HR HTTP request blocked](images/hr-http-blocked.png)

![IT HTTP access allowed](images/IT-can-access-server.png)

## Outcome

The ACL restricted a specific application without blocking legitimate network diagnostics. This demonstrates service-level filtering using protocol, source, destination and port criteria.

## Skills demonstrated

Extended ACLs · TCP port filtering · HTTP access control · ICMP · Static server addressing · Interface direction · Application-level validation

[Back to Networking projects](../)
