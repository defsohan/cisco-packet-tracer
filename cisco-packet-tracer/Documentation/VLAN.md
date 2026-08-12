# VLANs & Inter-VLAN Routing

## What a VLAN Does

A VLAN (Virtual LAN) creates a separate broadcast domain within a switch, logically grouping ports regardless of physical location. Devices in different VLANs cannot communicate without a routing device (router or L3 switch), even if plugged into the same physical switch.

## Access Ports vs. Trunk Ports

| Port Type | Purpose | Config |
|---|---|---|
| Access | Connects to a single end device (PC, printer, server), carries traffic for exactly one VLAN | `switchport mode access` / `switchport access vlan <id>` |
| Trunk | Carries traffic for multiple VLANs between switches (or to a router), tags frames with 802.1Q | `switchport mode trunk` / `switchport trunk allowed vlan <list>` |

## Creating a VLAN

```
vlan 10
 name SALES
```

## Assigning an Access Port

```
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
```

## Configuring a Trunk

```
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 switchport trunk native vlan 99
```

> **Native VLAN:** untagged traffic on a trunk belongs to the native VLAN. Best practice is to set it to an unused VLAN (not VLAN 1) to reduce VLAN-hopping risk.

## Inter-VLAN Routing — Two Approaches

**Router-on-a-Stick** (one physical router interface, multiple subinterfaces):
```
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
```

**Layer 3 Switch (SVI)** — requires `ip routing` enabled:
```
ip routing
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
```

Router-on-a-stick is simpler to set up in a lab but bottlenecks all inter-VLAN traffic through one physical link. L3 switching scales better for real deployments. See [Inter-VLAN-Routing project](../Projects/Inter-VLAN-Routing) for a full worked comparison.

## Verification Commands

```
show vlan brief
show interfaces trunk
show interfaces switchport
```
