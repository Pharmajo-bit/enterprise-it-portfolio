# Dynamic Routing with OSPF

## Summary

Configured OSPF Area 0 between Cisco routers, verified neighbour formation and confirmed that remote networks were learned dynamically.

| Item | Details |
|---|---|
| Protocol | OSPFv2 |
| Area | 0 |
| Platform | Cisco Packet Tracer |
| Verification | Interface status, running configuration, neighbours, routes and ping |

## Business requirement

The routed network needed to exchange reachability information automatically. Static routes would create additional administrative work and would not adapt efficiently as the topology changed.

## Implementation

### 1. Configure routed interfaces

Assigned IP addresses to each router interface and confirmed that the links were operational.

![Interface status](images/show-ip-interface-brief.png)

### 2. Enable OSPF

Configured OSPF and advertised the connected networks into Area 0. Passive-interface settings were used where neighbour relationships were not required.

![OSPF configuration](images/show-running-config-ospf.png)

### 3. Verify neighbour formation

Confirmed that directly connected routers reached the expected OSPF adjacency state.

![OSPF neighbours](images/show-ip-ospf-neighbor.png)

### 4. Verify dynamic routes

Reviewed the routing table for OSPF-learned routes to remote networks.

![OSPF routes](images/show-ip-route.png)

## Topology and validation

![Network topology](images/network-topology.png)

| Check | Result |
|---|---|
| Routed interfaces up/up | Pass |
| OSPF process and Area 0 configured | Pass |
| Neighbour adjacency established | Pass |
| Remote routes marked as OSPF-learned | Pass |
| End-to-end connectivity successful | Pass |

![OSPF connectivity test](images/ospf-connectivity-test.png)

## Outcome

Routers exchanged network information dynamically and provided end-to-end connectivity without static routes. Verification confirmed both control-plane adjacency and data-plane forwarding.

## Skills demonstrated

OSPFv2 · Area 0 · Network advertisement · Passive interfaces · Neighbour analysis · Routing tables · Cisco IOS verification · Connectivity testing

[Back to Networking projects](../)
