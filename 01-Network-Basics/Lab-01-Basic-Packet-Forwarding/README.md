# Lab 01 - Basic Packet Forwarding

## Overview

This lab demonstrates the fundamentals of packet forwarding between two IPv4 networks connected through a Cisco ISR 4331 router.

The primary objective was to understand how Ethernet frames and IPv4 packets are processed at Layer 2 and Layer 3 by observing ARP and ICMP behavior in both local and remote network communication.

The topology was implemented in Cisco Packet Tracer using Cisco Catalyst 3560-24PS switches connected to the router via fiber optic links through SFP interfaces.

---

## Objectives

- Build a network consisting of two different IPv4 subnets.
- Configure router interfaces with IPv4 addresses.
- Configure static IPv4 addresses on all end devices.
- Configure default gateways manually.
- Establish communication between two different networks through a router.
- Analyze ARP behavior within the same subnet.
- Analyze ARP behavior when communicating with a remote subnet.
- Observe ICMP packet forwarding using Packet Tracer Simulation Mode.
- Verify MAC address learning on switches.
- Verify routing information on the router.

---

## Network Topology

> Insert the topology screenshot here.

---

## Network Architecture

The topology contains two independent IPv4 LANs connected by a Cisco ISR 4331 router.

- Left LAN: 192.168.10.0/24
- Right LAN: 192.168.20.0/24

Each LAN is connected through Cisco Catalyst 3560-24PS switches. The router performs Layer 3 forwarding between the two networks, while the switches provide Layer 2 connectivity within each subnet.

---

## Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|---------|-----------|------------|-------------|-----------------|
| Router | G0/0/0 | 192.168.10.1 | 255.255.255.0 | - |
| Router | G0/0/1 | 192.168.20.1 | 255.255.255.0 | - |
| PC10L | Fa0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC11L | Fa0 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC12L | Fa0 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC13L | Fa0 | 192.168.10.13 | 255.255.255.0 | 192.168.10.1 |
| PC10R | Fa0 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC11R | Fa0 | 192.168.20.11 | 255.255.255.0 | 192.168.20.1 |

---

## Configuration Summary

The following tasks were completed during this lab:

1. Designed and built a topology consisting of two independent IPv4 subnets.
2. Connected the Cisco Catalyst 3560-24PS switch to the Cisco ISR 4331 router using SFP fiber interfaces.
3. Assigned static IPv4 addresses to all end devices.
4. Configured IPv4 addresses on both router interfaces.
5. Enabled the router interfaces using the `no shutdown` command.
6. Configured the default gateway on each end device.
7. Verified local and remote connectivity using ICMP Echo Requests.
8. Observed ARP and ICMP packet flow using Packet Tracer Simulation Mode.
9. Examined the router routing table and switch MAC address tables.

---

## Verification

The following verification steps were successfully completed:

- Verified communication between hosts within the same subnet.
- Verified communication between hosts located in different subnets.
- Captured and analyzed ARP Request and ARP Reply packets.
- Captured and analyzed ICMP Echo Request and Echo Reply packets.
- Verified MAC address learning on the switches.
- Verified the router's directly connected routes.

---

## Key Concepts Learned

This lab helped reinforce several fundamental networking concepts:

- ARP is responsible for resolving IPv4 addresses into MAC addresses.
- ARP requests are limited to the local broadcast domain.
- When the destination device belongs to another subnet, the sender does not resolve the destination MAC address. Instead, it resolves the MAC address of the default gateway.
- Switches forward Ethernet frames based on their MAC Address Tables.
- Routers forward packets based on their Routing Tables rather than MAC addresses.
- ICMP provides end-to-end connectivity testing using Echo Request and Echo Reply messages.
- Packet forwarding between different networks requires Layer 3 routing.

---

## Challenges and Troubleshooting

While building the topology, the router and switch initially failed to establish a physical connection.

After investigation, the issue was traced to incompatible SFP transceivers installed on the devices.

A second issue occurred because the router interface supported both RJ-45 copper and SFP fiber media. The interface required manual media selection using the `media-type sfp` command before the fiber link became operational.

This experience reinforced the importance of validating physical-layer connectivity before troubleshooting upper-layer protocols.

---

## Useful Commands

### Verification Commands

```bash
show ip interface brief
show ip route
show arp
show mac address-table
```

### Configuration Commands

```bash
interface GigabitEthernet0/0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/0/1
 ip address 192.168.20.1 255.255.255.0
 no shutdown

media-type sfp
```

---

## Lessons Learned

This lab demonstrated the relationship between Layer 2 and Layer 3 communication.

Before an ICMP packet can be transmitted, the sender must first determine the correct destination MAC address. If the destination is located within the same subnet, ARP resolves the destination host's MAC address. If the destination belongs to a different subnet, ARP resolves the MAC address of the default gateway instead.

This lab also highlighted the importance of verifying physical connectivity and interface configuration before troubleshooting higher-layer networking issues.
