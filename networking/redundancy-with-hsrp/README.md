# HSRP Default-Gateway Redundancy

## Summary

Configured two routers to share a virtual default gateway, failed the active router, verified automatic takeover by the standby router and confirmed failback through preemption.

| Item | Details |
|---|---|
| Routers | 2 × Cisco 2911 |
| Switch | Cisco 2960 |
| Protocol | HSRP, group 1 |
| LAN | `192.168.10.0/24` |
| Virtual gateway | `192.168.10.1` |
| Platform | Cisco Packet Tracer |

## Business requirement

The LAN depended on one physical router as its default gateway. Hosts needed a stable gateway address and continued service if the preferred router or its LAN interface failed.

## Design

| Device | Address | Role |
|---|---|---|
| Virtual gateway | `192.168.10.1` | Client default gateway |
| R1 | `192.168.10.2` | Preferred active, priority 110 |
| R2 | `192.168.10.3` | Standby, priority 100 |

![HSRP topology](images/network-topology.png)

## Implementation

Both routers joined HSRP group 1 using the shared virtual address:

```text
standby 1 ip 192.168.10.1
```

R1 was made the preferred router and configured to reclaim the active role after recovery:

```text
standby 1 priority 110
standby 1 preempt
```

`show standby brief` confirmed R1 as Active and R2 as Standby.

![R1 active](images/R1-active-role.png)

![R2 standby](images/R2-standby-role.png)

## Failure and recovery testing

### 1. Establish a baseline

PC1 successfully reached the virtual gateway with no packet loss.

![Normal gateway connectivity](images/normal-connectivity.png)

### 2. Fail the active router

Shut down R1's LAN-facing interface. R1 left the active state and R2 transitioned from Standby to Active.

![R1 interface failure](images/R1-down.png)

![R2 active after failure](images/R2-active-role.png)

### 3. Confirm service recovery

PC1 continued using `192.168.10.1`. One of four pings timed out during the transition, after which connectivity resumed through R2.

![Connectivity after failover](images/PC1-still-pings.png)

### 4. Restore and preempt

Restored R1. Its higher priority and `preempt` configuration allowed it to progress back to Active, returning R2 to Standby.

![R1 active after recovery](images/R1-active-role-again.png)

| Test | Result |
|---|---|
| R1 initially active and R2 standby | Pass |
| Virtual gateway reachable | Pass |
| R2 assumes active role after failure | Pass |
| Client gateway remains unchanged | Pass |
| Connectivity resumes automatically | Pass |
| R1 reclaims active role after recovery | Pass |

## Outcome

HSRP removed the physical router address as the client's single point of dependency. The test demonstrated automatic failover, a brief measured interruption and successful failback to the preferred router.

## Skills demonstrated

HSRP · Virtual gateways · Priority · Preemption · State analysis · Active/standby redundancy · Failure simulation · Failover and failback testing

[Back to Networking projects](../)
