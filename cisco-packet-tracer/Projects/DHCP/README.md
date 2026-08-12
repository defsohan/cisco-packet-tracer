# DHCP

**Status:** 🔜 Scaffolded — full write-up pending

## Focus

DHCP configuration for automatic IP assignment — both router-based DHCP pools and a dedicated DHCP server, including DHCP relay (`ip helper-address`) for VLANs not directly on the DHCP server's subnet.

## Planned Contents

- [ ] Topology diagram
- [ ] DHCP pool/scope table (network, range, exclusions, DNS, gateway)
- [ ] Device list
- [ ] Configuration commands (DHCP pool, relay)
- [ ] Connectivity testing (lease verification via `ipconfig`, `show ip dhcp binding`)
- [ ] Key concepts learned

## Key Concepts (to demonstrate)

- Router-based DHCP pool configuration
- DHCP relay across VLANs/subnets
- Excluded address ranges (for static devices like servers/printers)
- Lease verification and troubleshooting
