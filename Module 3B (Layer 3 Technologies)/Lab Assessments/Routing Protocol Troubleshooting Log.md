# Routing Protocol Troubleshooting Log

## Initial Problem Report
**Start Time:** 10:08 AM
**Symptoms:**
- Internet connectivity lost from Area 1
- BGP routes missing from routing table  
- OSPF adjacency down between ABRs
- Routing loop detected in Area 2
- Suboptimal path selection to remote sites

## Phase 1: Assessment (0-20 minutes)
### Quick Status Check
- [x] OSPF neighbor states (show ip ospf neighbor)
- [x] BGP session status (show ip bgp summary)  
- [x] Routing table analysis (show ip route)
- [x] Interface status verification
- [x] Routing protocol process status

### Initial Findings:
1. ABR2 had mismatched hello/dead timers to it's neighbors. One configured for 10/40, the other 30/120.
2. OSPF areas not traversing the backbone area as needed.
3. OSPF not redistributed into BGP routing table

## Phase 2/3: Resolution

1. Reconfigured ABR1 to match in terms of hello/dead timers. Using default broadcast / point-to-point timers of 10/40 rather than 30/120 for non-broadcast.
2. Configured the advertised network on the interface from ABR2 connecting to the neighboring backbone router to use area 0 (needed). Was not configured akin to this prior.
3. Redistributed a single loopback OSPF network on ABR1 to test if redistributing ospf into BGP would work.