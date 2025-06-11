# Lab01_Routage de deux réseaux via un routeur

## Objectif  
Configurer et tester la connectivité entre deux réseaux distincts interconnectés par un routeur Cisco.

## Matériel  
- Routeur Cisco (ISR 920)  
- Deux switches  
- Deux PC connectés en mode accès  
- Réseau 192.168.1.0/24 (PC0)  
- Réseau 192.168.2.0/24 (PC1)

## Configuration principale  
- Configuration des interfaces du routeur avec adresses IP  
- Connexion de chaque réseau à une interface du routeur  
- Configuration IP des PC avec passerelle correspondante  
- Vérification de la connectivité inter-réseaux

## Commandes principales  
```bash
enable
configure terminal
hostname R1

interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface GigabitEthernet0/0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

end
write memory
```
## Configuration PC ##
PC Réseau 1 : IP 192.168.1.10 /24, passerelle 192.168.1.1
PC Réseau 2 : IP 192.168.2.10 /24, passerelle 192.168.2.1

## Tests ##
Ping inter-réseau entre les deux PC pour valider le routage.
