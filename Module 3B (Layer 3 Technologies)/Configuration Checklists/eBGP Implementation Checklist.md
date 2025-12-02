# eBGP Implementation Checklist

## BGP Neighbor Establishment
- [X] All eBGP neighbors established (show ip bgp summary)
- [X] BGP session states all "Established"
- [X] Correct neighbor AS numbers configured
- [X] Authentication working if configured
- [X] TTL security preventing session hijacking

## Route Advertisement and Receipt
- [X] Each AS advertising intended networks
- [X] Route filtering preventing unwanted advertisements
- [X] Default route received from ISP (AS 65004)
- [X] No accidental transit traffic flowing
- [X] BGP table showing expected routes (show ip bgp)

## Path Selection Verification
- [X] Best path selection following BGP algorithm
- [X] Local preference modifications working
- [X] AS-path prepending affecting path selection
- [X] Backup paths available during failures

## Traffic Engineering Testing
- [X] Primary path traffic measurement
- [X] Failover scenario testing
- [X] Policy routing integration tested