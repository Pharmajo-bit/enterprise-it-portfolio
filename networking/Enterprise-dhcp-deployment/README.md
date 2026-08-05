# Case Study 07 - Enterprise DHCP Deployment

## Overview

This project demonstrates the implementation of Dynamic Host Configuration Protocol (DHCP) within a segmented enterprise network. DHCP services were configured on a Cisco router to automatically assign IP addresses, subnet masks, default gateways and DNS settings to client devices across multiple VLANs.

---

## Business Scenario

As the organisation expanded, manually assigning IP addresses to every workstation became inefficient and increased the risk of addressing errors and duplicate IP conflicts.

To simplify administration and improve scalability, DHCP was deployed so that devices automatically received the correct network configuration based on their departmental VLAN.

---

## Objectives

- Configure DHCP services on the Cisco router.
- Create separate DHCP pools for HR, IT and Finance.
- Reserve gateway addresses from dynamic allocation.
- Automatically assign IP addresses to client devices.
- Verify successful DHCP lease allocation.
- Validate end-to-end network connectivity.

---

## Environment

| Component | Configuration |
|-----------|---------------|
| Router | Cisco 2911 |
| Switch | Cisco Catalyst 2960 |
| DHCP Server | Cisco IOS Router |
| VLAN 10 | HR |
| VLAN 20 | IT |
| VLAN 30 | Finance |
| Simulation Platform | Cisco Packet Tracer |

---

## Network Topology

The existing enterprise network was used as the foundation for the DHCP deployment.

![Network Topology](images/network-topology.png)

---

## Implementation

### DHCP Pool Configuration

Separate DHCP pools were created for each departmental VLAN. Each pool defined the network address, default gateway and DNS server. Infrastructure addresses were excluded to prevent conflicts with the router interfaces.

**Evidence**

**Figure 1 – DHCP Pool Configuration**

![DHCP Pool](images/show-ip-dhcp-pool.png)

---

### Dynamic Address Allocation

Each workstation was configured to obtain its network configuration automatically. Devices successfully received addresses from the appropriate DHCP pool based on their VLAN membership.

**Evidence**

**Figure 2 – HR Workstation**

![HR DHCP](images/hr-ipconfig.png)

**Figure 3 – IT Workstation**

![IT DHCP](images/it-ipconfig.png)

**Figure 4 – Finance Workstation**

![Finance DHCP](images/finance-ipconfig.png)

---

### DHCP Lease Verification

The DHCP binding table was examined to confirm that leases had been successfully issued to all client devices.

**Evidence**

**Figure 5 – DHCP Lease Bindings**

![DHCP Binding](images/show-ip-dhcp-binding.png)

---

## Validation

Connectivity testing confirmed that all departmental devices successfully communicated after automatically receiving their network configuration.

**Evidence**

**Figure 6 – Successful Inter-VLAN Connectivity**

![Connectivity](images/inter-vlan-connectivity.png)

---

## Outcome

The implementation successfully automated IP address management across multiple VLANs. Devices received consistent network settings without manual configuration, reducing administrative overhead while improving scalability and maintainability.

---

## Skills Demonstrated

- Cisco IOS DHCP
- DHCP Pool Configuration
- DHCP Lease Management
- Automatic IP Address Allocation
- Enterprise IP Address Management
- Router-on-a-Stick
- Network Validation
- Cisco IOS Verification Commands

---

## Lessons Learned

- DHCP automates IP address management and reduces manual configuration.
- Separate DHCP pools provide appropriate network settings for different VLANs.
- Excluding infrastructure addresses prevents IP conflicts.
- DHCP lease verification confirms successful address assignment.
- Connectivity testing validates that DHCP integrates correctly with existing network services.
