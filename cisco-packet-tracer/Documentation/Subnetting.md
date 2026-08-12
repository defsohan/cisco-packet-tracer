# Subnetting & CIDR

## Why Subnet

Splitting a large network into smaller subnets reduces broadcast domain size, improves security through segmentation (see [VLAN.md](./VLAN.md)), and makes more efficient use of address space.

## CIDR Notation

CIDR notation (`/24`, `/26`, etc.) states how many bits of the 32-bit address are the network portion.

| CIDR | Subnet Mask | Hosts per Subnet |
|---|---|---|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 (point-to-point links, e.g. router-to-router WAN) |

## Quick Subnetting Method

1. Determine how many hosts each subnet needs
2. Find the smallest block size that fits (`2^n - 2` usable hosts, where n = host bits)
3. Subtract that CIDR from 32 to get the mask
4. The "magic number" (block size) = 256 − (last octet of the mask)

**Example:** need 50 hosts per subnet
- `2^6 - 2 = 62` ≥ 50 → 6 host bits → /26 (255.255.255.192)
- Magic number = 256 − 192 = 64
- Subnets: `.0`, `.64`, `.128`, `.192` — each with 62 usable hosts

## Worked Example (used in Enterprise-Network project)

Requirement: 3 department subnets (Sales, IT, Management), each needing fewer than 254 hosts, plus a /30 for the router-to-router WAN link.

| Subnet | CIDR | Range | Usable Hosts |
|---|---|---|---|
| Sales (VLAN 10) | 192.168.10.0/24 | .1 – .254 | 254 |
| IT (VLAN 20) | 192.168.20.0/24 | .1 – .254 | 254 |
| Management (VLAN 30) | 192.168.30.0/24 | .1 – .254 | 254 |
| WAN link (R1–R2) | 203.0.113.0/30 | .1 – .2 | 2 |

## VLSM (Variable Length Subnet Masking)

Using different subnet sizes for different needs instead of one fixed mask everywhere — e.g. a /30 for a point-to-point WAN link instead of wasting a /24 on a link that only needs 2 addresses. Used throughout this repo's WAN links.
