# IP Addressing

## IPv4 Address Structure

An IPv4 address is 32 bits, written as 4 octets (e.g. `192.168.10.1`). Split into a **network portion** and a **host portion**, determined by the subnet mask.

| Class | Range | Default Mask | Typical Use |
|---|---|---|---|
| A | 1.0.0.0 – 126.255.255.255 | /8 | Very large networks |
| B | 128.0.0.0 – 191.255.255.255 | /16 | Medium networks |
| C | 192.0.0.0 – 223.255.255.255 | /24 | Small networks (most LAN design) |

## Private Address Ranges (RFC 1918)

| Range | CIDR | Common Use |
|---|---|---|
| 10.0.0.0 – 10.255.255.255 | /8 | Large enterprise networks |
| 172.16.0.0 – 172.31.255.255 | /12 | Medium networks |
| 192.168.0.0 – 192.168.255.255 | /16 | Small/home/lab networks — used throughout this repo |

## Static vs. Dynamic Addressing

- **Static:** manually configured, used for infrastructure devices (routers, switches, servers) so their address never changes
- **Dynamic (DHCP):** automatically assigned, used for end-user devices — see [DHCP project](../Projects/DHCP)

## IPv6 Basics

- 128-bit address, written in 8 groups of hex separated by colons (e.g. `2001:db8::1`)
- Leading zeros in a group can be omitted, and one run of consecutive all-zero groups can be collapsed to `::` (only once per address)
- No broadcast — uses multicast and anycast instead
- Link-local addresses (`fe80::/10`) are automatically assigned to every interface

## Assigning Addresses on Cisco IOS

```
interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown
```

See [Subnetting.md](./Subnetting.md) for how to calculate ranges and masks.
