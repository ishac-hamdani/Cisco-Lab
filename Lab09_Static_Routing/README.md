# Lab09_Static_Routing

## Description  
Ce lab met en œuvre un routage statique entre deux réseaux via un routeur Cisco. Le routeur R1 joue également le rôle de serveur DHCP pour le réseau local.

## Topologie  
- **R1**
  - G0/0/0 : 192.168.10.1/30 (vers R2)
  - G0/0/1 : 192.168.1.1/24 (LAN1)
- **R2**
  - G0/0/0 : 192.168.10.2/30 (vers R1)
  - G0/0/1 : 192.168.2.1/24 (LAN2)
- **PC0** (réseau 192.168.1.0/24, DHCP)
- **PC1** (réseau 192.168.2.0/24, IP statique)

## Objectifs  
- Activer le routage statique entre deux réseaux
- Configurer un pool DHCP pour LAN1
- Vérifier la connectivité inter-réseaux

## Configuration R1
```bash
hostname R1

interface GigabitEthernet0/0/0
 ip address 192.168.10.1 255.255.255.252
 no shutdown

interface GigabitEthernet0/0/1
 ip address 192.168.1.1 255.255.255.0
 no shutdown

ip dhcp excluded-address 192.168.1.1

ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1

ip route 192.168.2.0 255.255.255.0 192.168.10.2

banner motd ^CIshac-LAB^C
```
###Configuration R2
```bash
enable
configure terminal
hostname R2
interface GigabitEthernet0/0/0
 ip address 192.168.10.2 255.255.255.252
 no shutdown
exit
interface GigabitEthernet0/0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit

ip route 192.168.1.0 255.255.255.0 192.168.10.1
```
###Adressage PC
PC0 (LAN1) : DHCP, reçoit une IP dans 192.168.1.0/24
PC1 (LAN2) : IP statique 192.168.2.10, masque /24, passerelle 192.168.2.1

###Tests
ping entre PC0 et PC1
show ip route sur chaque routeur
Vérification des baux DHCP avec show ip dhcp binding

###Remarque
Ce lab montre un routage statique minimal avec distribution IP dynamique d’un côté. Utile pour illustrer la base du routage inter-réseaux sans protocole dynamique.
