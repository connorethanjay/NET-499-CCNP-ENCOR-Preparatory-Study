## Phase 2: Problem Isolation (20-50 minutes)
### Issue #1: Customer A GRE Tunnel
**Root Cause:** Tunnel mode was misconfigured on Customer A
**Commands Used:** do show interface tunnel0

### Issue #2: Customer B Encryption
**Root Cause:** ISAKMP key was not matching on both hosts.
**Commands Used:** do show run, crypto isakmp key Cisco123! address xxx.xxx.xxx.xxx

## Phase 3: Resolution (50-80 minutes)
### Fixes Applied:
1. **Issue:** Tunnel mode was misconfigured on Customer A
   **Solution:** tunnel mode gre ip
   **Verification:** do show interface tunnel0

2. **Issue:** ISAKMP key was not matching on both hosts.
   **Solution:** crypto isakmp key Cisco123! address xxx.xxx.xxx.xxx
   **Verification:** do show run

## Phase 4: Final Verification (80-90 minutes)
- [x] All customer VRFs isolated
- [x] GRE tunnels operational
- [x] IPSec encryption working
- [ ] Route leaking functioning
- [ ] End-to-end connectivity confirmed

### Did not get to work on the VRFs for this lab. Wanted to focus on them in the other VRF labs.