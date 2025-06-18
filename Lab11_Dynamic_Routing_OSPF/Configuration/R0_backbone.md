# Lab11_Dynamic_Routing_OSPF

## Configuration R0

```bash
hostname R0

interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
 shutdown

interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown

interface GigabitEthernet0/2
 no ip address
 duplex auto
 speed auto
 shutdown

interface Serial0/0/0
 ip address 192.168.10.2 255.255.255.252
 ip ospf 1 area 0
 no shutdown

interface Serial0/0/1
 ip address 192.168.20.2 255.255.255.252
 ip ospf 1 area 0
 no shutdown

interface Serial0/1/0
 ip address 192.168.30.2 255.255.255.252
 ip ospf 1 area 0
 no shutdown

interface Serial0/1/1
 ip address 192.168.40.2 255.255.255.252
 ip ospf 1 area 0
 no shutdown

interface Vlan1
 no ip address
 shutdown

router ospf 1
 router-id 0.0.0.1
 log-adjacency-changes

ip classless

line con 0
line aux 0
line vty 0 4
 login
```
