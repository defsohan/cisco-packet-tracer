# Basic Network Security

## Access Control Lists (ACLs)

Filter traffic based on source/destination address, protocol, and port. See [Routing.md](./Routing.md) for the difference between standard and extended ACLs, and the [ACL project](../Projects/ACL) for a full worked example.

**Key rule:** ACLs process top-down with an implicit deny at the end — order matters, and more specific rules must come before broader ones.

## Port Security

Restricts which/how many MAC addresses can connect to a switch port — protects against unauthorized devices and basic MAC flooding attacks.

```
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security mac-address sticky
 switchport port-security violation shutdown
```

| Violation Mode | Behavior |
|---|---|
| `protect` | Drops traffic from violating MAC, no log, port stays up |
| `restrict` | Drops traffic from violating MAC, logs violation, port stays up |
| `shutdown` (default) | Port goes err-disabled, requires manual `shutdown`/`no shutdown` to recover |

## Device Hardening Basics

```
! Encrypt passwords stored in config
service password-encryption

! Set enable secret (encrypted) instead of enable password (plaintext)
enable secret <password>

! Restrict remote access to SSH only
line vty 0 4
 transport input ssh
 login local

! Local user for SSH
username admin secret <password>

! Banner (legal notice, not "welcome")
banner motd #Authorized access only#
```

## NAT as a Security Boundary

While NAT's primary purpose is address conservation, PAT/overload also means internal hosts aren't directly reachable from outside without an explicit port forward — a secondary (not primary) security benefit. See [NAT project](../Projects/NAT).

## VLAN Segmentation as Security

Separating traffic by department/function (see [VLAN.md](./VLAN.md)) limits blast radius — a compromised device in one VLAN can't directly reach another VLAN without passing through a routed, filterable boundary (where ACLs can then be applied).

## Spanning Tree Protocol (STP) — Security Angle

Beyond loop prevention, STP hardening features reduce attack surface on access ports:

```
interface FastEthernet0/1
 spanning-tree portfast
 spanning-tree bpduguard enable
```

`bpduguard` shuts down a port if it receives a BPDU — protecting against a rogue switch being connected to an access port.

## Scope Note

This document covers switch/router-level security fundamentals demonstrated in this repo. It is not a substitute for a full security posture (firewalls, IDS/IPS, endpoint protection) in a production environment.
