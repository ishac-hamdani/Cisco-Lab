# Lab11_Dynamic_Routing_OSPF

## Configuration R3
```bash 
hostname R3

ip dhcp excluded-address 192.168.3.1

ip dhcp pool LAN3
 network 192.168.3.0 255.255.255.0
 default-router 192.168.3.1
 dns-server 8.8.8.8

interface GigabitEthernet0/0
 ip address 192.168.3.1 255.255.255.0
 ip ospf 1 area 3
 no shutdown

interface Serial0/0/0
 ip address 192.168.30.1 255.255.255.252
 ip ospf 1 area 0
 no shutdown

router ospf 1
 router-id 3.3.3.3
 log-adjacency-changes

banner motd ^CIshac-LAB^C
```
