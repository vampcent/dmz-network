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
*Full Cisco IOS ACL commands to be added upon completion*