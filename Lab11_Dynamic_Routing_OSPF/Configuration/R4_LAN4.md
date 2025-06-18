# Lab11_Dynamic_Routing_OSPF

## Configuration R4
```bash 
hostname R4
ip dhcp excluded-address 192.168.4.1

ip dhcp pool LAN4
 network 192.168.4.0 255.255.255.0
 default-router 192.168.4.1
 dns-server 8.8.8.8

interface GigabitEthernet0/0
 ip address 192.168.4.1 255.255.255.0
 ip ospf 1 area 4
 no shutdown

interface Serial0/0/0
 ip address 192.168.40.1 255.255.255.252
 ip ospf 1 area 0
 no shutdown

router ospf 1
 router-id 4.4.4.4
 log-adjacency-changes

banner motd ^CIshac-LAB^C
```
