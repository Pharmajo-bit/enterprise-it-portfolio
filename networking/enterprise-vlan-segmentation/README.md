# Enterprise VLAN Segmentation and Inter-VLAN Routing

## Summary

Segmented HR, IT and Finance into separate VLANs and enabled communication between them using an 802.1Q trunk and router-on-a-stick routing.

| Item | Details |
|---|---|
| Router | Cisco 2911 |
| Switch | Cisco Catalyst 2960 |
| Platform | Cisco Packet Tracer |
| VLAN 10 | HR |
| VLAN 20 | IT |
| VLAN 30 | Finance |
| Routing | Router-on-a-stick |

## Business requirement

A growing organisation needed separate broadcast domains for each department while retaining authorised inter-department communication. The design also needed to provide a foundation for DHCP and traffic-control policies.

## Implementation

### 1. Create and assign VLANs

Created the three departmental VLANs and assigned access ports according to each workstation's department.

![VLAN configuration](images/sh-vlan-brief.png)

### 2. Configure the trunk

Configured the switch-to-router link as an IEEE 802.1Q trunk so all departmental VLANs could share the physical uplink.

![Trunk verification](images/sh-int-trunk.png)

### 3. Configure inter-VLAN routing

Created router subinterfaces with an IP gateway for each VLAN.

![Router subinterfaces](images/sh-ip-int-brief.png)

## Topology and validation

![Network topology](images/network-topology.png)

| Test | Result |
|---|---|
| VLANs present on the switch | Pass |
| Access ports assigned correctly | Pass |
| 802.1Q trunk operational | Pass |
| Router subinterfaces up | Pass |
| Inter-VLAN ping successful | Pass |

![Successful inter-VLAN connectivity](images/inter-vlan-ping.png)

## Outcome

The three departments were logically separated while remaining reachable through Layer 3 routing. The design established a scalable base for DHCP, ACL and redundancy projects.

## Skills demonstrated

Cisco VLANs · Access ports · 802.1Q trunking · Router-on-a-stick · Inter-VLAN routing · Layer 2 switching · Layer 3 routing · Connectivity testing

[Back to Networking projects](../)
