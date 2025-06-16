# Lab10_Dynamic_Routing_RIP - Configuration d’un routage dynamique grâce à RIP

## Objectif  
Configurer un réseau avec 3 LAN reliés par 3 routeurs Cisco via RIP. Chaque LAN a un PC en DHCP.

## Topologie
Routeur	LAN IP	Interface LAN	Interfaces séries
R1	192.168.1.0/24	GigabitEthernet0/0	Serial0/0/0 (192.168.10.1/30), Serial0/1/1 (192.168.30.1/30)
R2	192.168.2.0/24	GigabitEthernet0/0	Serial0/0/0 (192.168.10.2/30), Serial0/0/1 (192.168.20.1/30)
R3	192.168.3.0/24	GigabitEthernet0/0	Serial0/0/1 (192.168.20.2/30), Serial0/1/1 (192.168.30.2/30)

## Configuration DHCP
```bash
R1
ip dhcp excluded-address 192.168.1.1
ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
R2

nginx
Copier
Modifier
ip dhcp excluded-address 192.168.2.1
ip dhcp pool LAN2
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
R3

nginx
Copier
Modifier
ip dhcp pool LAN3
 network 192.168.3.0 255.255.255.0
 default-router 192.168.3.1
Configuration Interfaces
R1

nginx
Copier
Modifier
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface Serial0/0/0
 ip address 192.168.10.1 255.255.255.252
 no shutdown

interface Serial0/1/1
 ip address 192.168.30.1 255.255.255.252
 no shutdown

R2
interface GigabitEthernet0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown

interface Serial0/0/0
 ip address 192.168.10.2 255.255.255.252
 no shutdown

interface Serial0/0/1
 ip address 192.168.20.1 255.255.255.252
 no shutdown

R3
interface GigabitEthernet0/0
 ip address 192.168.3.1 255.255.255.0
 no shutdown

interface Serial0/0/1
 ip address 192.168.20.2 255.255.255.252
 no shutdown

interface Serial0/1/1
 ip address 192.168.30.2 255.255.255.252
 no shutdown
Configuration RIP (version 2)

R1
router rip
 version 2
 no auto-summary
 network 192.168.1.0
 network 192.168.10.0
 network 192.168.30.0

R2
router rip
 version 2
 no auto-summary
 network 192.168.2.0
 network 192.168.10.0
 network 192.168.20.0

R3
router rip
 version 2
 no auto-summary
 network 192.168.3.0
 network 192.168.20.0
 network 192.168.30.0
```

## Vérifications
- Vérifier que les PCs ont une IP via DHCP
- Ping inter-LAN (ex: PC R1 → PC R2, R3)
- show ip route rip sur chaque routeur
- show ip protocols pour voir RIP actif
## Topologie  
- Routeur connecté au switch via GigabitEthernet0/0/0  
- PC1 et PC2 connectés au switch  
- Réseau : 192.168.1.0/24  
- Passerelle : 192.168.1.1  
- DNS : 8.8.8.8  
- Plage DHCP : 192.168.1.11 à 192.168.1.254  
- Adresses exclues : 192.168.1.1 à 192.168.1.10  

## Étapes de configuration
```bash
enable
configure terminal

banner motd 'Ishac-LAB'

interface GigabitEthernet0/0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
 exit

ip dhcp excluded-address 192.168.1.1 192.168.1.10

ip dhcp pool LAN
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
 exit

write memory
```

