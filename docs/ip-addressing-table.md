# IP Addressing Table

## DMZ Zone
| Device | Interface | IP Address | Subnet Mask |
|--------|-----------|------------|-------------|
| Internet router | Fa0/0 | 203.0.113.1 | 255.255.255.252 |
| Border router | Fa0/0 (outside) | 203.0.113.2 | 255.255.255.252 |
| Border router | Fa0/1 (DMZ) | 172.16.10.1 | 255.255.255.0 |
| Web server | NIC | 172.16.10.2 | 255.255.255.0 |
| DNS server | NIC | 172.16.10.3 | 255.255.255.0 |

## Internal LAN
| Device | Interface | IP Address | Subnet Mask |
|--------|-----------|------------|-------------|
| Border router | Fa0/2 (LAN) | 192.168.0.1 | 255.255.255.0 |

## VLAN 10 – HR (192.168.10.0/24)
| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| HR PC 1 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| HR PC 2 | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 |
| HR printer | 192.168.10.4 | 255.255.255.0 | 192.168.10.1 |
| HR wireless AP | 192.168.10.5 | 255.255.255.0 | 192.168.10.1 |

## VLAN 20 – IT (192.168.20.0/24)
| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| IT PC 1 | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| IT PC 2 | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 |
| IT wireless AP | 192.168.20.4 | 255.255.255.0 | 192.168.20.1 |

## VLAN 30 – Finance (192.168.30.0/24)
| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| Finance laptop 1 | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |
| Finance laptop 2 | 192.168.30.3 | 255.255.255.0 | 192.168.30.1 |
| Finance wireless AP | 192.168.30.4 | 255.255.255.0 | 192.168.30.1 |

## VLAN 40 – Shared Resources (192.168.40.0/24)
| Device | IP Address | Subnet Mask | Default Gateway |
|--------|------------|-------------|-----------------|
| Shared printer | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 |