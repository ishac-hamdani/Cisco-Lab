# Lab11_Dynamic_Routing_OSPF  
## Configuration R1
```bash
hostname R1

ip dhcp excluded-address 192.168.1.1

ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8

interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 ip ospf 1 area 1

interface Serial0/0/0
 ip address 192.168.10.1 255.255.255.252
 ip ospf 1 area 0


router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes

banner motd ^CIshac-LAB^C

```
