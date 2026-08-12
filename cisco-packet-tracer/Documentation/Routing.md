# Routing — Static & Dynamic

## Static Routing

Manually configured routes — full administrative control, no protocol overhead, but doesn't adapt to topology changes and doesn't scale well past a handful of routers.

```
ip route <destination-network> <subnet-mask> <next-hop-or-exit-interface>

! Example
ip route 192.168.20.0 255.255.255.0 203.0.113.2

! Default route (gateway of last resort)
ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

## Dynamic Routing Protocol Comparison

| Protocol | Type | Metric | Notes |
|---|---|---|---|
| RIP | Distance-vector | Hop count (max 15) | Simple, largely obsolete for real networks, useful for learning fundamentals |
| OSPF | Link-state | Cost (based on bandwidth) | Industry-standard interior gateway protocol, fast convergence, supports areas |
| EIGRP | Advanced distance-vector (Cisco proprietary) | Composite (bandwidth + delay) | Fast convergence, easier to configure than OSPF, Cisco-only |

## OSPF Essentials

```
router ospf 1
 network <network> <wildcard-mask> area <area-id>
```

Neighbor adjacency requires matching: **area ID, subnet, MTU, hello/dead timers, and authentication (if configured).**

Verification:
```
show ip ospf neighbor
show ip route ospf
show ip protocols
```

## EIGRP Essentials

```
router eigrp <AS-number>
 network <network> <wildcard-mask>
```

Neighbors must share the same **AS number** and be on the same subnet.

Verification:
```
show ip eigrp neighbors
show ip route eigrp
```

## Administrative Distance (Why It Matters)

When multiple routing sources learn the same route, the router trusts the one with the **lowest** administrative distance:

| Source | Default AD |
|---|---|
| Directly connected | 0 |
| Static route | 1 |
| EIGRP | 90 |
| OSPF | 110 |
| RIP | 120 |

This is why a static route will always override a dynamically learned route to the same destination unless explicitly configured otherwise (floating static routes use a higher AD for exactly this reason — as a backup path).

## Verifying the Routing Table

```
show ip route
```
Look at the leftmost letter code (`C` connected, `S` static, `O` OSPF, `D` EIGRP) to identify how each route was learned.
