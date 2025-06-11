# Lab03_VLANs - Routage Inter-VLAN avec Switch Layer 3

## Objectif  
Configurer et tester le routage inter-VLAN permettant la communication entre plusieurs VLANs distincts via un switch Layer 3.

## Matériel  
- Switch Cisco Layer 3 (exemple Catalyst 3560/3750)  
- PC connectés sur des ports en mode accès  
- VLAN 10 (Professeur), VLAN 20 (Etudiant)  

## Configuration principale  
- Création des VLANs  
- Assignation des ports en mode accès aux VLANs  
- Configuration des interfaces VLAN (SVI) avec adresses IP  
- Activation du routage inter-VLAN (`ip routing`)  
- Configuration IP des PC avec passerelle correspondante  

## Commandes principales  
```bash
enable
configure terminal

vlan 10
name Professeur
exit

vlan 20
name Etudiant
exit

interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
exit

interface vlan 10
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface vlan 20
ip address 192.168.20.1 255.255.255.0
no shutdown
exit

ip routing
exit

write memory
```

## Configuration PC  
- PC VLAN 10 : IP 192.168.10.x /24, passerelle 192.168.10.1  
- PC VLAN 20 : IP 192.168.20.x /24, passerelle 192.168.20.1  

## Tests  
- Ping inter-VLAN entre PC des VLANs différents pour valider le routage.
