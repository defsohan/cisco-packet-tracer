# Network Troubleshooting

## General Approach

1. **Layer 1** — Is the physical link up? (`show interfaces`, check for `up/up` status, cable/port errors)
2. **Layer 2** — Is switching correct? (VLAN assignment, trunk config, MAC address table, STP state)
3. **Layer 3** — Is routing correct? (IP addressing, routing table, gateway configuration)
4. **Layer 4+** — Is a filter blocking it? (ACLs, NAT misconfiguration, firewall rules)

Working bottom-up avoids chasing a routing issue that's actually a duplex mismatch at Layer 1.

## Common Issues & Fixes (from this repo's projects)

| Symptom | Likely Cause | Fix |
|---|---|---|
| Interface shows `administratively down` | Interface not enabled | `no shutdown` |
| PC can't reach anything, not even the gateway | No IP address, wrong subnet mask, or gateway not set | Verify with `ipconfig` / `show ip interface brief` |
| Devices in the same VLAN can't communicate | Access port assigned to wrong VLAN | `show vlan brief`, correct with `switchport access vlan <id>` |
| Inter-VLAN traffic doesn't route | Subinterface encapsulation set but parent interface down, or SVI missing `ip routing` | `no shutdown` on parent; confirm `ip routing` enabled on L3 switch |
| OSPF neighbors stuck in `EXSTART`/`EXCHANGE` | MTU mismatch | Match MTU on both interfaces |
| OSPF neighbors never form | Area ID mismatch or wrong wildcard mask in `network` statement | Verify with `show ip ospf interface brief` |
| NAT not translating | `ip nat inside`/`ip nat outside` reversed | Apply `inside` to LAN-facing interface, `outside` to WAN-facing |
| ACL blocking more than intended | Missing specific permit before a broader deny (ACLs are processed top-down, first match wins) | Reorder — most specific rules first |
| Port shuts down (err-disabled) after connecting a device | Port security violation (max MAC exceeded) | `shutdown` / `no shutdown` to reset, verify device's MAC, adjust `switchport port-security maximum` if needed |
| DHCP client not getting an address across VLANs | Missing DHCP relay | Add `ip helper-address <dhcp-server-ip>` on the VLAN's SVI/subinterface |

## Key Verification Commands

```
show ip interface brief      ! Quick status of every interface
show interfaces <int>        ! Detailed Layer 1/2 stats, errors
show vlan brief               ! VLAN-to-port assignment
show interfaces trunk         ! Trunk status and allowed VLANs
show ip route                 ! Routing table
show ip ospf neighbor         ! OSPF adjacency status
show ip eigrp neighbors       ! EIGRP adjacency status
show ip nat translations      ! Active NAT translations
show access-lists             ! ACL hit counters
show port-security interface  ! Port security status and violations
```

## Testing Tools

- `ping` — Layer 3 reachability
- `traceroute` — path and hop-by-hop latency/failure point
- `telnet <ip> <port>` — quick Layer 4 port reachability check (useful before assuming a service is down)
