# Layer 2 Troubleshooting Scenario
<!--Troubleshooting issues with Commonality Lab Physical infrastructure-->
## Initial Problem Report
**Start Time:** [6:15PM]

**Symptoms Reported:**
- Hosts in VLAN 90 cannot reach external networks
- 1 of 2 EtherChannels between DIST-SW-02 and ACC-SW-02 showing as down
- Some access ports not getting DHCP
- Broadcast storms suspected

## Phase 1: Problem Identification (0-15 minutes)
### Quick Assessment
- [X] Physical connectivity status 
- [X] VLAN database consistency check
- [X] Trunk port status review
- [X] EtherChannel status verification
- [X] STP topology analysis

### Initial Findings:

1. **Issue**: Hosts on VLAN 90 eg. MGMT VMs cannot reach the internet.
   Evidence: WSRV-MGMT.internal.commonalitylab.com cannot ping 8.8.8.8 or google.com.

2. **Issue**: Etherchannel Link between DIST-SW-02 and ACC-SW-02 is improperly configured.
   Evidence: On DIST-SW-02, Etherchannel #7 uses interfaces G6/0/33-36. On ACC-SW-02, Etherchannels #3 and #4 are configured for G0/33-34, and G0/35-36.

3. **Issue**: CORE-SWITCH-STACK is not configured as the root bridge(s). 
   Evidence: Using "show spanning-tree summary", the CORE-SWITCH-STACK does not display as the root bridge while using MST.

## Phase 2: Detailed Analysis (15-75 minutes)
### VLAN Issues
**Problem:** Hosts from VLAN 90 could not access the internet.

**Root Cause:** VLAN 56 and VLAN 90 on the CORE-SW-STACK were configured to use the same subnet of 10.100.90.X (instead of 10.100.56.X & 10.100.90.X)

**Commands Used:** show vlan, show interfaces trunk

**Solution:** Change the IP Address of VLAN 56 on CORE-SW-STACK to 10.100.56.243/24, create new VLAN 90 SVI on CORE-SW-STACK, and set IP Address of 10.100.90.243/24

### EtherChannel Issues  
**Problem:** Etherchannel Misconfiguration

**Root Cause:** On DSW2, Etherchannel #7 uses interfaces G6/0/33-36 instead of two separate Etherchannel Links.

**Commands Used:** show etherchannel summary, interface range g6/0/35-36, (no) channel-group **X** mode active

**Solution:** Creating new port-channel #8 using interfaces g6/0/35-36. 

### STP Issues
**Problem:** Core Switch Stack is not the root bridge for MST in the network.

**Root Cause:** When enabling MST, none of the pre-configured priority values carried over.

**Commands Used:** spanning-tree mst **XX** priority **XXXX**, show spanning-tree summary

**Solution:** Manually setting MST priority for all switches in increments of 4096 to match previously configured STP priority.

## Phase 3: Final Verification (75-90 minutes)
- [x] All VLANs communicating properly
- [X] EtherChannel operational and load balancing
- [X] STP topology optimized
- [X] No broadcast storms detected
- [X] End-to-end connectivity confirmed