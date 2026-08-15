# OSPF Dynamic Routing and Network Redundancy

## Overview

This project demonstrates the implementation of **OSPF (Open Shortest Path First)** in a redundant four-router network using Cisco Packet Tracer.

The network was configured with two equal-cost paths between two LANs. OSPF was used to dynamically advertise routes, establish neighbor relationships, and maintain connectivity when one of the network paths failed.

---

## Business Scenario

A network requires reliable communication between two separate LANs.

Rather than relying on a single route between the networks, a redundant topology was implemented with two possible paths between R1 and R4.

OSPF was deployed so that routers could dynamically learn available networks and automatically respond to changes in the topology.

The design was then tested by deliberately removing one of the available paths and verifying that traffic continued through the remaining route without manual routing changes.

---

## Objectives

- Configure IPv4 addressing across the network
- Implement `/30` point-to-point router links
- Configure single-area OSPF
- Establish OSPF neighbor adjacencies
- Verify dynamically learned routes
- Test communication between separate LANs
- Verify equal-cost OSPF routing
- Simulate a network link failure
- Validate automatic OSPF failover

---

## Environment

| Component | Details |
|---|---|
| Platform | Cisco Packet Tracer |
| Routers | 4 × Cisco 2911 |
| End Devices | 2 × PCs |
| Routing Protocol | OSPF |
| OSPF Area | Area 0 |
| Router Links | /30 |
| LAN Networks | /24 |

---

## Network Topology

The network was designed using a diamond topology, providing two possible paths between R1 and R4.

![Complete Network Topology](images/complete-network-topology.png)

The two available paths are:

```text
R1 → R2 → R4
R1 → R3 → R4
```

This redundant design allows traffic to continue reaching the destination if one of the paths becomes unavailable.

---

## IP Addressing Plan

The router-to-router connections use `/30` subnets, providing two usable host addresses for each point-to-point link.

The LANs use `/24` networks.

| Device | Connection | IP Address |
|---|---|---|
| R1 | R1-R2 | 10.0.12.2/30 |
| R1 | R1-R3 | 10.0.13.2/30 |
| R1 | LAN | 192.168.10.1/24 |
| R2 | R2-R1 | 10.0.12.1/30 |
| R2 | R2-R4 | 10.0.24.1/30 |
| R3 | R3-R1 | 10.0.13.1/30 |
| R3 | R3-R4 | 10.0.34.1/30 |
| R4 | R4-R2 | 10.0.24.2/30 |
| R4 | R4-R3 | 10.0.34.2/30 |
| R4 | LAN | 192.168.20.1/24 |
| PC1 | LAN | 192.168.10.2/24 |
| PC2 | LAN | 192.168.20.2/24 |

### Default Gateways

| Device | Default Gateway |
|---|---|
| PC1 | 192.168.10.1 |
| PC2 | 192.168.20.1 |

---

# Implementation

## 1. Interface Configuration

IPv4 addresses were assigned to each router interface according to the addressing plan.

Interface status was verified using:

```bash
show ip interface brief
```

![R1 Interface Verification](images/initial-ip-brief(1).png)

The output from R1 confirmed that all three required interfaces were operational in the `up/up` state.

This verified the interface configuration before implementing and testing OSPF.

---

## 2. OSPF Configuration

OSPF process **1** was configured across the routers using **Area 0**.

Example configuration from R1:

```bash
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.13.0 0.0.0.3 area 0
```

![R1 OSPF Configuration](images/section-router-ospf(1).png)

Each router advertised its directly connected networks into OSPF.

The `/30` point-to-point networks used the wildcard mask:

```text
0.0.0.3
```

The `/24` LAN networks used:

```text
0.0.0.255
```

---

## 3. OSPF Neighbor Formation

OSPF neighbor relationships were verified using:

```bash
show ip ospf neighbor
```

![OSPF Neighbor Verification](images/ospf%20neighbor(1).png)

R1 successfully established `FULL` OSPF adjacencies with both neighboring routers.

This confirmed that R1 was successfully exchanging OSPF information with R2 and R3.

---

# Validation

## 1. OSPF Route Verification

The route from R1 to the remote `192.168.20.0/24` LAN was examined using:

```bash
show ip route 192.168.20.0
```

![OSPF Route Before Failure](images/sh-ip-route-before-failure(1).png)

R1 learned two routes to the remote network:

```text
via 10.0.12.1
via 10.0.13.1
```

Both routes had an OSPF metric of **3** and a traffic share count of **1**.

This confirmed that OSPF had installed two **equal-cost paths**:

```text
R1 → R2 → R4
R1 → R3 → R4
```

Because both paths had the same calculated OSPF cost, both were installed in the routing table.

This demonstrates **Equal-Cost Multi-Path (ECMP)** routing.

---

## 2. End-to-End Connectivity

Connectivity between the two LANs was tested from PC1 (`192.168.10.2`) to PC2 (`192.168.20.2`).

The following commands were used:

```bash
ping 192.168.20.2
tracert 192.168.20.2
```

![End-to-End Connectivity Test](images/end-to-end-connectivity-test-before-failure(1).png)

PC1 successfully reached PC2 across the routed network.

The successful ping confirmed end-to-end Layer 3 connectivity between the two LANs.

The traceroute also demonstrated that traffic was being forwarded through the OSPF-enabled network to reach the remote destination.

---

## 3. Link Failure Test

To test network redundancy, the connection between **R1 and R2** was deliberately taken down.

Before the failure, two paths were available:

```text
R1 → R2 → R4
R1 → R3 → R4
```

After removing the R1-R2 connection, only the lower path remained available.

![Network Topology After Failure](images/network-topology-after-failure(1).png)

No static route was added and no manual change was made to the existing OSPF configuration.

OSPF was allowed to automatically respond to the topology change.

---

## 4. OSPF Failover Verification

After the R1-R2 connection became unavailable, the route to the remote LAN was checked again:

```bash
show ip route 192.168.20.0
```

![OSPF Route After Failure](images/after-R2-failure(1).png)

Before the failure, R1 had two equal-cost routes:

```text
via 10.0.12.1
via 10.0.13.1
```

After the failure, the route through R2 (`10.0.12.1`) was removed.

Only the route through R3 remained:

```text
via 10.0.13.1
```

Traffic could therefore continue using the remaining path:

```text
R1 → R3 → R4
```

This confirmed that OSPF automatically adapted to the topology change and maintained a valid route to the remote network.

---

## Outcome

The network successfully established dynamic routing between all four routers using OSPF.

Under normal operation, R1 learned two equal-cost routes to the remote `192.168.20.0/24` LAN:

```text
R1 → R2 → R4
R1 → R3 → R4
```

When the R1-R2 connection was deliberately removed, OSPF automatically removed the unavailable path from the routing table.

Traffic could continue through:

```text
R1 → R3 → R4
```

This demonstrated that the redundant network design and OSPF dynamic routing could maintain connectivity following a link failure without requiring manual route changes.

---

## Skills Demonstrated

- Cisco IOS configuration
- IPv4 addressing and subnetting
- `/30` point-to-point subnet design
- OSPF configuration
- OSPF Area 0
- OSPF neighbor verification
- Dynamic route analysis
- Equal-Cost Multi-Path (ECMP) routing
- Routing table interpretation
- Network redundancy
- Failover testing
- Ping and traceroute verification
- Cisco Packet Tracer

---

## Lessons Learned

This project reinforced how OSPF dynamically learns and maintains routing information rather than relying on manually configured routes.

The redundant topology demonstrated that OSPF can install multiple routes to the same destination when the calculated path costs are equal.

The failure test demonstrated the practical benefit of combining dynamic routing with network redundancy. When one path became unavailable, OSPF updated the routing table and continued forwarding traffic through the remaining available path without requiring manual intervention.

The project also reinforced the importance of validating a network using OSPF neighbor states, routing tables, ping tests, and traceroute rather than assuming that a successful configuration alone means the network is operating correctly.
