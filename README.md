# Inter-VLAN Routing Implementation Using Router-on-a-Stick

## Overview
Designed and implemented inter-VLAN routing in a segmented network environment using a single router interface with subinterfaces (Router-on-a-Stick). Enabled controlled communication between isolated VLANs while maintaining segmentation at Layer 2.

## Objective
Configured and deployed inter-VLAN routing to enable communication between VLAN 10 HR and VLAN 20 IT through a centralized routing point, enforcing structured traffic flow between segmented networks.

## Network Setup
Devices Used
1 Cisco 2960 Switch
1 Cisco 1941 Router
2 End Devices PCs

Topology Design
PCs connected to switch access ports
Switch uplink FastEthernet0/24 connected to router GigabitEthernet0/0
VLAN segmentation applied at the switch level
Routing performed at the router via subinterfaces


![Network Topology](https://github.com/Pelumi-Johnson/Inter-VLAN-Routing-Implementation-Using-Router-on-a-Stick/blob/main/Screenshot%202026-04-03%20020457.png)

## Configuration

### VLAN Segmentation Pre existing
- VLAN 10 assigned to HR devices
- VLAN 20 assigned to IT devices
- VLAN 30 assigned to FINANCE devices

![VLAN Configuration](https://github.com/Pelumi-Johnson/Inter-VLAN-Routing-Implementation-Using-Router-on-a-Stick/blob/main/Screenshot%202026-04-03%20020847.png)

### Trunk Configuration Switch
Configured the switch uplink port to operate in trunk mode to carry multiple VLANs to the router

enable
configure terminal
interface fastEthernet 0/24
switchport mode trunk
exit

![Trunk Port](https://github.com/Pelumi-Johnson/Inter-VLAN-Routing-Implementation-Using-Router-on-a-Stick/blob/main/Screenshot%202026-04-03%20021314.png)

### Router Subinterface Configuration
Implemented Router on a Stick by creating subinterfaces for each VLAN and assigning gateway IP addresses

enable
configure terminal
interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface gigabitEthernet 0/0
no shutdown

Screenshot Placeholder Router Subinterfaces
![Router Subinterfaces](./screenshots/router-subinterfaces.png)

### End Device IP Configuration
VLAN 10 HR
IP 192.168.10.10
Gateway 192.168.10.1

VLAN 20 IT
IP 192.168.20.10
Gateway 192.168.20.1

Screenshot Placeholder PC Configuration
![PC IP Config](./screenshots/pc-ip-config.png)

## Validation
Performed connectivity testing to verify inter VLAN communication

Initiated ICMP test from VLAN 10 to VLAN 20
Confirmed successful packet transmission via router

ping 192.168.20.10

Screenshot Placeholder Successful Ping
![Ping Success](./screenshots/ping-success.png)

## Key Concepts Applied
VLAN segmentation to isolate broadcast domains
802.1Q trunking to transport multiple VLANs across a single link
Router on a Stick architecture for inter VLAN routing
Subinterface configuration for VLAN specific gateways
Default gateway implementation for cross network communication
Layer 2 and Layer 3 traffic control separation

## Outcome
Established controlled communication between isolated VLANs using centralized routing
Maintained segmentation while enabling inter department connectivity reflecting real world enterprise network design where isolation and communication are both intentionally enforced

## Failure Testing and Troubleshooting
Simulated misconfigurations to validate network dependency on correct setup

Removed trunk configuration resulting in VLAN traffic failing to reach router
Incorrect default gateway preventing hosts from routing traffic
Missing encapsulation dot1Q preventing router from identifying VLAN traffic

Verified and restored functionality through targeted troubleshooting

Screenshot Placeholder Failure Scenario
![Failure Test](./screenshots/failure-test.png)

## Project Summary
Implemented a scalable inter VLAN routing solution enabling secure and structured communication across segmented networks
Demonstrated practical configuration validation and troubleshooting aligned with real world network engineering practices
