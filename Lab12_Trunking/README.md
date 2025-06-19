# Lab – Routage Inter-VLAN avec Router-on-a-Stick (Lab12_Trunking)
## Objectif
Configurer le routage inter-VLAN via un seul port trunk entre le routeur et le switch. Les clients obtiennent leur IP par DHCP.

## Définition
Router-on-a-Stick : méthode où un seul port physique du routeur gère plusieurs VLANs grâce à des sous-interfaces (dot1Q).

## Topologie
- Routeur : R0
- Switch : 2960
- VLAN 10 → 192.168.10.0/24 → PC0
- VLAN 20 → 192.168.20.0/24 → PC1
- Port Fa0/1 entre routeur et switch = trunk

## Configuration
### Routeur R0
```bash 
hostname R0

ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1

ip dhcp pool VLAN20
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1

interface GigabitEthernet0/0
 no ip address

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```
### Switch
```bash
vlan 10
 name VLAN10

vlan 20
 name VLAN20

interface fa0/2
 switchport mode access
 switchport access vlan 10

interface fa0/3
 switchport mode access
 switchport access vlan 20

interface fa0/1
 switchport mode trunk
```
### Tests de vérification
- PC0 et PC1 obtiennent leur IP via DHCP.
- Ping entre les deux PC : OK.
- Communication VLAN ↔ VLAN fonctionne via le routeur.
