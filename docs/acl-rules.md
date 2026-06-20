# ACL Rules & Security Policy

## Security Design Principles
This network follows the principle of least privilege - devices and 
departments are only granted access to the resources they need, and nothing more.

## Zone Security Rules
| Rule | Source | Destination | Action |
|------|--------|-------------|--------|
| 1 | Internet | DMZ (HTTP/DNS) | Allow |
| 2 | Internet | Internal LAN | Deny |
| 3 | Internal LAN | DMZ | Allow |
| 4 | Internal LAN | Internet (via NAT) | Allow |
| 5 | DMZ | Internal LAN | Deny |

## Inter-VLAN Rules
| Rule | Source VLAN | Destination VLAN | Action |
|------|------------|-----------------|--------|
| 1 | VLAN 20 (IT) | VLAN 40 (Shared) | Allow |
| 2 | VLAN 30 (Finance) | VLAN 40 (Shared) | Allow |
| 3 | VLAN 10 (HR) | VLAN 40 (Shared) | Deny |
| 4 | Any VLAN | Any other VLAN | Deny |

## Security Decisions
- HR is denied access to the shared printer as it is only required
  by IT and Finance
- VLANs are isolated by default to prevent lateral movement between
  departments in the event of a security breach
- The DMZ cannot initiate connections to the internal LAN, preventing
  a compromised DMZ server from attacking internal resources
- NAT hides internal IP addresses from the outside internet

## ACL Configuration

### INTER-VLAN ACL (applied to Gi0/2.10)
ip access-list extended INTER-VLAN

deny ip 192.168.10.0 0.0.0.255 192.168.40.0 0.0.0.255

permit ip 192.168.20.0 0.0.0.255 192.168.40.0 0.0.0.255

permit ip 192.168.30.0 0.0.0.255 192.168.40.0 0.0.0.255

permit ip any any

### OUTSIDE-IN ACL (applied to Gi0/0)
ip access-list extended OUTSIDE-IN

permit tcp any 172.16.10.0 0.0.0.255 eq 80

permit tcp any 172.16.10.0 0.0.0.255 eq 443

permit udp any 172.16.10.0 0.0.0.255 eq 53

deny ip any 192.168.0.0 0.0.255.255

permit ip any any

### DMZ-IN ACL (applied to Gi0/1)
ip access-list extended DMZ-IN

permit tcp 172.16.10.0 0.0.0.255 192.168.0.0 0.0.255.255 established

deny ip 172.16.10.0 0.0.0.255 192.168.0.0 0.0.255.255

permit ip any any

## Important Note on DMZ-IN Rule
The DMZ-IN ACL permits established TCP connections from the DMZ back 
to the internal LAN. This allows internal devices to receive replies 
from the web server while still preventing the DMZ from initiating 
new connections to the internal LAN. This is a stateless ACL 
workaround since Cisco IOS ACLs on Packet Tracer do not support 
stateful inspection.