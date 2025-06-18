# Lab11_Dynamic_Routing_OSPF

## Configuration R2

```bash
hostname R2

ip dhcp excluded-address 192.168.2.1

ip dhcp pool LAN1
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
 dns-server 8.8.8.8

interface GigabitEthernet0/0
 ip address 192.168.2.1 255.255.255.0
 ip ospf 1 area 2
 no shutdown

interface Serial0/0/0
 ip address 192.168.20.1 255.255.255.252
 ip ospf 1 area 0
 no shutdown

router ospf 1
 router-id 2.2.2.2
 log-adjacency-changes

banner motd ^CIshac-LAB^C
```
