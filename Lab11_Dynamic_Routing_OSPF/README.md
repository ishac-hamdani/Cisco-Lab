# Lab – Routage Dynamique avec OSPF (Multi-area)

## Objectif  
Configurer un réseau multi-areas avec le protocole OSPF. Chaque routeur gère un LAN avec des clients en DHCP.

## Topologie  
Routeur	LAN IP	            Interface LAN	        Interfaces séries  
- R1	    192.168.1.0/24	    GigabitEthernet0/0	    Serial0/0/0 (192.168.10.1/30)  
- R2	    192.168.2.0/24	    GigabitEthernet0/0	    Serial0/0/0 (192.168.10.2/30), Serial0/0/1 (192.168.20.1/30)  
- R3	    192.168.3.0/24	    GigabitEthernet0/0	    Serial0/0/1 (192.168.20.2/30), Serial0/1/1 (192.168.30.2/30)  
- R4	    192.168.4.0/24	    GigabitEthernet0/0	    Serial0/1/1 (192.168.30.1/30)  

## Configuration DHCP
### R1
```bash
ip dhcp excluded-address 192.168.1.1
ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
```
### R2
```bash
ip dhcp excluded-address 192.168.2.1
ip dhcp pool LAN2
 network 192.168.2.0 255.255.255.0
 default-router 192.168.2.1
```
### R3
```bash
ip dhcp excluded-address 192.168.3.1
ip dhcp pool LAN3
 network 192.168.3.0 255.255.255.0
 default-router 192.168.3.1
```
### R4
```bash
ip dhcp excluded-address 192.168.4.1
ip dhcp pool LAN4
 network 192.168.4.0 255.255.255.0
 default-router 192.168.4.1
```
## Configuration des interfaces
### R1
```bash
interface GigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface Serial0/0/0
 ip address 192.168.10.1 255.255.255.252
 no shutdown
```
### R2
interface GigabitEthernet0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown
interface Serial0/0/0
 ip address 192.168.10.2 255.255.255.252
 no shutdown
interface Serial0/0/1
 ip address 192.168.20.1 255.255.255.252
 no shutdown
 
### R3
```bash
interface GigabitEthernet0/0
 ip address 192.168.3.1 255.255.255.0
 no shutdown
interface Serial0/0/1
 ip address 192.168.20.2 255.255.255.252
 no shutdown
interface Serial0/1/1
 ip address 192.168.30.2 255.255.255.252
 no shutdown
```
### R4
```bash
interface GigabitEthernet0/0
 ip address 192.168.4.1 255.255.255.0
 no shutdown
interface Serial0/1/1
 ip address 192.168.30.1 255.255.255.252
 no shutdown
```
## Configuration OSPF
### R1
```bash
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 1
 network 192.168.10.0 0.0.0.3 area 0
```
### R2
```bash
router ospf 1
 router-id 2.2.2.2
 network 192.168.2.0 0.0.0.255 area 2
 network 192.168.10.0 0.0.0.3 area 0
 network 192.168.20.0 0.0.0.3 area 0
```
### R3
```bash
router ospf 1
 router-id 3.3.3.3
 network 192.168.3.0 0.0.0.255 area 3
 network 192.168.20.0 0.0.0.3 area 0
 network 192.168.30.0 0.0.0.3 area 0
```
### R4
```bash
router ospf 1
 router-id 4.4.4.4
 network 192.168.4.0 0.0.0.255 area 4
 network 192.168.30.0 0.0.0.3 area 0
```
 
## Vérifications
- Vérifier que les PC reçoivent une IP via DHCP
- Ping inter-LAN (ex : PC1 → PC2 → PC3 → PC4)
- show ip route ospf sur chaque routeur
- show ip ospf neighbor pour vérifier les adjacences
- show ip protocols pour vérifier les routes apprises
