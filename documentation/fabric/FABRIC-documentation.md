# FABRIC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| FABRIC | l3leaf | DC1-LEAF1A | 10.31.100.101/24 | vEOS-lab | Provisioned |
| FABRIC | l3leaf | DC1-LEAF1B | 10.31.100.102/24 | vEOS-lab | Provisioned |
| FABRIC | l3leaf | DC1-LEAF2A | 10.31.100.103/24 | vEOS-lab | Provisioned |
| FABRIC | l3leaf | DC1-LEAF2B | 10.31.100.104/24 | vEOS-lab | Provisioned |
| FABRIC | l3leaf | DC1-SPINE1 | 10.31.100.111/24 | vEOS-lab | Provisioned |
| FABRIC | l3leaf | DC1-SPINE2 | 10.31.100.112/24 | vEOS-lab | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | DC1-LEAF1A | Ethernet1 | l3leaf | DC1-SPINE1 | Ethernet1 |
| l3leaf | DC1-LEAF1A | Ethernet2 | l3leaf | DC1-SPINE2 | Ethernet1 |
| l3leaf | DC1-LEAF1A | Ethernet7 | mlag_peer | DC1-LEAF1B | Ethernet7 |
| l3leaf | DC1-LEAF1A | Ethernet8 | mlag_peer | DC1-LEAF1B | Ethernet8 |
| l3leaf | DC1-LEAF1B | Ethernet1 | l3leaf | DC1-SPINE1 | Ethernet2 |
| l3leaf | DC1-LEAF1B | Ethernet2 | l3leaf | DC1-SPINE2 | Ethernet2 |
| l3leaf | DC1-LEAF2A | Ethernet1 | l3leaf | DC1-SPINE1 | Ethernet3 |
| l3leaf | DC1-LEAF2A | Ethernet2 | l3leaf | DC1-SPINE2 | Ethernet3 |
| l3leaf | DC1-LEAF2A | Ethernet7 | mlag_peer | DC1-LEAF2B | Ethernet7 |
| l3leaf | DC1-LEAF2A | Ethernet8 | mlag_peer | DC1-LEAF2B | Ethernet8 |
| l3leaf | DC1-LEAF2B | Ethernet1 | l3leaf | DC1-SPINE1 | Ethernet4 |
| l3leaf | DC1-LEAF2B | Ethernet2 | l3leaf | DC1-SPINE2 | Ethernet4 |
| l3leaf | DC1-SPINE1 | Ethernet1 | l3leaf | DC1-SPINE2 | Ethernet1 |
| l3leaf | DC1-SPINE1 | Ethernet7 | mlag_peer | DC1-SPINE2 | Ethernet7 |
| l3leaf | DC1-SPINE1 | Ethernet8 | mlag_peer | DC1-SPINE2 | Ethernet8 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.91.250.0/26 | 64 | 18 | 28.13 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| DC1-LEAF1A | Ethernet1 | 10.91.250.9/31 | DC1-SPINE1 | Ethernet1 | 10.91.250.4/31 |
| DC1-LEAF1A | Ethernet2 | 10.91.250.11/31 | DC1-SPINE2 | Ethernet1 | 10.91.250.10/31 |
| DC1-LEAF1B | Ethernet1 | 10.91.250.13/31 | DC1-SPINE1 | Ethernet2 | 10.91.250.12/31 |
| DC1-LEAF1B | Ethernet2 | 10.91.250.15/31 | DC1-SPINE2 | Ethernet2 | 10.91.250.6/31 |
| DC1-LEAF2A | Ethernet1 | 10.91.250.17/31 | DC1-SPINE1 | Ethernet3 | 10.91.250.16/31 |
| DC1-LEAF2A | Ethernet2 | 10.91.250.19/31 | DC1-SPINE2 | Ethernet3 | 10.91.250.18/31 |
| DC1-LEAF2B | Ethernet1 | 10.91.250.21/31 | DC1-SPINE1 | Ethernet4 | 10.91.250.20/31 |
| DC1-LEAF2B | Ethernet2 | 10.91.250.23/31 | DC1-SPINE2 | Ethernet4 | 10.91.250.22/31 |
| DC1-SPINE1 | Ethernet1 | 10.91.250.4/31 | DC1-SPINE2 | Ethernet1 | 10.91.250.10/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.91.250.64/27 | 32 | 6 | 18.75 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | DC1-LEAF1A | 10.91.250.67/32 |
| FABRIC | DC1-LEAF1B | 10.91.250.68/32 |
| FABRIC | DC1-LEAF2A | 10.91.250.69/32 |
| FABRIC | DC1-LEAF2B | 10.91.250.70/32 |
| FABRIC | DC1-SPINE1 | 10.91.250.65/32 |
| FABRIC | DC1-SPINE2 | 10.91.250.66/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.91.250.96/27 | 32 | 6 | 18.75 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | DC1-LEAF1A | 10.91.250.99/32 |
| FABRIC | DC1-LEAF1B | 10.91.250.99/32 |
| FABRIC | DC1-LEAF2A | 10.91.250.101/32 |
| FABRIC | DC1-LEAF2B | 10.91.250.101/32 |
| FABRIC | DC1-SPINE1 | 10.91.250.97/32 |
| FABRIC | DC1-SPINE2 | 10.91.250.97/32 |
