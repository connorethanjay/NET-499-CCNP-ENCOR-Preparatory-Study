# VRF Implementation Verification Checklist

## Pre-Implementation Verification
- [x] All router interfaces are up/up
- [x] Base IP connectivity between routers confirmed
- [x] IOS version supports VRF (show version)

## VRF Configuration Verification
- [ ] VRFs created on all routers (show vrf)
- [ ] Interfaces assigned to correct VRFs (show ip vrf interfaces)
- [ ] IP addresses configured within VRFs (show ip route vrf [name])
- [ ] VRF route tables isolated (no cross-contamination)

## Connectivity Testing
- [ ] CUSTOMER_A can reach MGMT (route leaking works)
- [ ] CUSTOMER_B cannot reach CUSTOMER_A (isolation confirmed)
- [ ] CUSTOMER_B can reach MGMT (route leaking works)
- [ ] Ping tests document source/destination IPs and results

## Troubleshooting Commands Reference
- show vrf
- show ip vrf interfaces
- show ip route vrf [name]
- ping vrf [name] [destination]
- traceroute vrf [name] [destination]

## Configuration Backup
- [ ] All router configurations saved
- [ ] Configuration files stored in GitHub with proper naming
