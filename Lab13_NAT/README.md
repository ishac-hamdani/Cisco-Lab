# Lab13_NAT
## Objectif
Implémenter un NAT avec surcharge (PAT) entre un réseau local (LAN) et l’extérieur.

## Architecture
[PC1] -- [SW] -- [R1] -- [Server PT]
            |       |       |
        VLAN 1   NAT    IP Publique

PC1 :
- DHCP automatique depuis R1

R1 :

-  G0/0 → vers le serveur (NAT outside) – IP : 200.1.1.1/8

-  G0/1 → vers le LAN (NAT inside) – IP : 192.168.1.1/24

- Server PT : héberge helloworld.html

  ## Configuration
  ```bash
  enable
configure terminal

hostname R1

interface GigabitEthernet0/0
 ip address 200.1.1.1 255.0.0.0
 ip nat outside
exit

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
exit

! DHCP
ip dhcp excluded-address 192.168.1.1
ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1

! NAT
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface GigabitEthernet0/0 overload
exit 
banner motd ^CIshac-LAB^C
end
write memory
```
