# Access Control Lists (ACL)

**Status:** 🔜 Scaffolded — full write-up pending

## Focus

Traffic filtering using standard and extended ACLs, applied to control access between subnets/VLANs based on source, destination, and protocol/port.

## Planned Contents

- [ ] Topology diagram
- [ ] IP addressing table
- [ ] Device list
- [ ] Standard ACL configuration + use case
- [ ] Extended ACL configuration + use case
- [ ] Verification (`show access-lists`, connectivity tests)
- [ ] Key concepts learned

## Key Concepts (to demonstrate)

- Standard ACL (source-only filtering) vs. extended ACL (source, destination, protocol, port)
- ACL processing order — first match wins, implicit deny at the end
- Placement: standard ACLs close to destination, extended ACLs close to source
- Applying ACLs to an interface (`in` vs `out`)

A worked extended ACL example is already documented in [Enterprise-Network](../Enterprise-Network).
