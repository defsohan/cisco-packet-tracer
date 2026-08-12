<div align="center">

# Cisco Packet Tracer — Network Design & Configuration

**A practical portfolio of network design, configuration, and troubleshooting projects built in Cisco Packet Tracer.**

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco_Packet_Tracer-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)
![Networking](https://img.shields.io/badge/Networking-LAN%2FWAN-0d1b2a?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

</div>

---

## Introduction

This repository documents a series of hands-on network design and configuration projects built and tested in Cisco Packet Tracer — ranging from basic LAN setups to enterprise-scale topologies with VLANs, dynamic routing, NAT, ACLs, and wireless integration.

Each project simulates a real-world network scenario: designed from requirements, addressed and subnetted, configured device-by-device, tested for connectivity, and documented with the troubleshooting steps taken along the way. This isn't a dump of `.pkt` files — every project folder is written to be readable and useful on its own.

## Objectives

- Demonstrate practical, hands-on Cisco networking skills beyond theory
- Show a repeatable design process: requirements → addressing → configuration → testing → troubleshooting
- Build a growing reference of real device configurations for common network scenarios
- Document networking concepts in a way that's useful to revisit or share with others learning the same material

## Technologies & Tools

| Tool | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation & topology design |
| Cisco IOS (CLI) | Router & switch configuration |
| Wireshark | Packet-level connectivity verification (where applicable) |

## Networking Concepts Covered

`LAN/WAN Design` · `IP Addressing & Subnetting (CIDR)` · `VLANs & Inter-VLAN Routing` · `Trunking & Access Ports` · `DHCP` · `DNS` · `Static Routing` · `Dynamic Routing (RIP, OSPF, EIGRP)` · `NAT/PAT` · `ACLs` · `Port Security` · `STP` · `Wireless Networking` · `Server Configuration` · `IPv4 & IPv6` · `Network Troubleshooting` · `Basic Network Security`

## Repository Structure

```
cisco-packet-tracer/
├── README.md
├── LICENSE
├── Projects/
│   ├── Basic-Network/
│   ├── LAN-Network/
│   ├── VLAN/
│   ├── Inter-VLAN-Routing/
│   ├── DHCP/
│   ├── Static-Routing/
│   ├── OSPF/
│   ├── EIGRP/
│   ├── NAT/
│   ├── ACL/
│   ├── Wireless-Network/
│   ├── Enterprise-Network/    ← flagship project, fully documented
│   └── Advanced-Network/
├── Documentation/
│   ├── IP-Addressing.md
│   ├── Subnetting.md
│   ├── VLAN.md
│   ├── Routing.md
│   ├── Troubleshooting.md
│   └── Network-Security.md
└── Screenshots/
```

## Projects

| Project | Focus | Status |
|---|---|---|
| [Basic-Network](./Projects/Basic-Network) | Fundamental device connectivity, IP addressing | 🔜 In progress |
| [LAN-Network](./Projects/LAN-Network) | Single-site LAN design, switching basics | 🔜 In progress |
| [VLAN](./Projects/VLAN) | VLAN segmentation, trunking, access ports | 🔜 In progress |
| [Inter-VLAN-Routing](./Projects/Inter-VLAN-Routing) | Router-on-a-stick & L3 switch routing | 🔜 In progress |
| [DHCP](./Projects/DHCP) | DHCP server/relay configuration | 🔜 In progress |
| [Static-Routing](./Projects/Static-Routing) | Multi-router static route configuration | 🔜 In progress |
| [OSPF](./Projects/OSPF) | Dynamic routing with OSPF | 🔜 In progress |
| [EIGRP](./Projects/EIGRP) | Dynamic routing with EIGRP | 🔜 In progress |
| [NAT](./Projects/NAT) | NAT/PAT for internet simulation | 🔜 In progress |
| [ACL](./Projects/ACL) | Standard & extended ACL traffic filtering | 🔜 In progress |
| [Wireless-Network](./Projects/Wireless-Network) | AP/WLC configuration, wireless clients | 🔜 In progress |
| [**Enterprise-Network**](./Projects/Enterprise-Network) | **Full topology: VLANs, OSPF, NAT/PAT, ACLs, port security (~14 devices)** | ✅ **Complete — start here** |
| [Advanced-Network](./Projects/Advanced-Network) | Multi-site, redundancy, advanced scenarios | 🔜 Planned |

> Projects marked 🔜 are scaffolded with a documentation template, ready to be filled in as each is rebuilt/re-verified in Packet Tracer. Start with **Enterprise-Network** for a complete, fully worked example.

## Example: Network Topology

The Enterprise-Network project topology (see full write-up for the addressing table and configs):

![Topology Diagram](./Projects/Enterprise-Network/topology-diagram.svg)

## Example: Configuration Snippet

```
! Inter-VLAN routing on core router — subinterface config
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

## Testing & Troubleshooting

Every project's connectivity is verified using:
- `ping` and `traceroute` between VLANs/subnets
- Cisco IOS `show` commands (`show ip route`, `show vlan brief`, `show interfaces trunk`, `show ip ospf neighbor`, etc.)
- Documented troubleshooting notes for issues actually hit during configuration (see [Documentation/Troubleshooting.md](./Documentation/Troubleshooting.md))

## Learning Outcomes

- Practical fluency in Cisco IOS CLI configuration across routing and switching
- Ability to design an IP addressing/subnetting scheme from a set of requirements
- Understanding of how VLANs, trunking, and inter-VLAN routing fit together
- Hands-on experience with both static and dynamic routing protocols
- Applied basic network security: ACLs, port security, NAT boundary control

## Future Improvements

- Add IPv6 addressing to existing topologies
- Add STP configuration examples (PVST+, root bridge tuning)
- Expand Advanced-Network with multi-site VPN/redundancy scenarios
- Add packet capture (Wireshark) evidence alongside `show` command output

## Author

**Sohan Sardar** — Penetration Tester | CEH | Networking
[GitHub](https://github.com/defsohan) · [LinkedIn](https://linkedin.com/in/defsohan) · [Fiverr](https://fiverr.com/sohan_sardar)
