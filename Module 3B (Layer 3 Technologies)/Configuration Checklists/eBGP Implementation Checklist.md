# eBGP Implementation Checklist

## BGP Neighbor Establishment
- [ ] All eBGP neighbors established (show ip bgp summary)
- [ ] BGP session states all "Established"
- [ ] Correct neighbor AS numbers configured
- [ ] Authentication working if configured
- [ ] TTL security preventing session hijacking

## Route Advertisement and Receipt
- [ ] Each AS advertising intended networks
- [ ] Route filtering preventing unwanted advertisements
- [ ] Default route received from ISP (AS 65004)
- [ ] No accidental transit traffic flowing
- [ ] BGP table showing expected routes (show ip bgp)

## Path Selection Verification
- [ ] Best path selection following BGP algorithm
- [ ] Local preference modifications working
- [ ] AS-path prepending affecting path selection
- [ ] MED values influencing traffic engineering
- [ ] Backup paths available during failures

## Traffic Engineering Testing
- [ ] Primary path traffic measurement
- [ ] Failover scenario testing
- [ ] Load balancing verification (if configured)
- [ ] Policy routing integration tested