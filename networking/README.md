# Networking

This section documents Cisco Packet Tracer projects that progress from network segmentation and addressing through traffic control, dynamic routing and gateway redundancy.

The projects include configuration evidence, verification commands, end-to-end testing and, where applicable, controlled failure scenarios.

## Projects

| Project | What was implemented and tested |
|---|---|
| [Enterprise VLAN segmentation and inter-VLAN routing](enterprise-vlan-segmentation/) | Created departmental VLANs, configured 802.1Q trunking and implemented router-on-a-stick routing. |
| [Enterprise DHCP deployment](Enterprise-dhcp-deployment/) | Built separate DHCP pools for HR, IT and Finance, verified leases and tested client connectivity. |
| [Directional traffic control using extended ACLs](department-isolation-using-ACLs/) | Permitted HR-initiated ICMP traffic while preventing Finance from initiating traffic toward HR. |
| [Securing an internal web service with ACLs](secure-internal-web-access-with-ACLs/) | Allowed basic connectivity while restricting unauthorised HTTP access to a Finance application. |
| [Dynamic routing using OSPF](dynamic-routing-using-ospf/) | Configured OSPF Area 0, verified neighbour relationships and validated learned routes. |
| [OSPF redundancy and failover](dynamic-routing-using-ospf/network-redundancy/) | Implemented equal-cost redundant paths, introduced a failure and confirmed automatic route recovery. |
| [HSRP default-gateway redundancy](redundancy-with-hsrp/) | Configured active/standby gateways, validated failover and confirmed preemptive failback. |

## Skills demonstrated

- Cisco IOS configuration and verification
- VLANs and access-port assignment
- IEEE 802.1Q trunking
- Router-on-a-stick and inter-VLAN routing
- DHCP pools and lease verification
- Extended access control lists
- OSPF neighbour and route analysis
- Equal-Cost Multi-Path routing
- HSRP priority, preemption and state analysis
- Connectivity, failure and recovery testing

[Return to the portfolio homepage](../)
