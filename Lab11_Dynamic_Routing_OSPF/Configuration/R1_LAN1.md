# Lab11_Dynamic_Routing_OSPF  
## Configuration R1

```bash
# Lab11_Dynamic_Routing_OSPF  
## Configuration R1

```bash
hostname R1

ip dhcp excluded-address 192.168.1.1

ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8

no ip cef
no ipv6 cef

spanning-tree mode pvst

interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 ip ospf 1 area 1
 duplex auto
 speed auto

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
 ip address 192.168.10.1 255.255.255.252
 ip ospf 1 area 0
 clock rate 2000000

interface Serial0/0/1
 no ip address
 clock rate 2000000
 shutdown

interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown

interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown

interface Vlan1
 no ip address
 shutdown

router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes

banner motd ^CIshac-LAB^C

```
