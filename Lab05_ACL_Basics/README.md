# Lab05_ACL_Basics - Blocage ICMP selon l'adresse IP

## Objectif  
Configurer une ACL pour empêcher un PC spécifique (PC2) de faire des requêtes ICMP (ping), tout en laissant un autre PC (PC1) communiquer normalement.

## Matériel  
- Routeur Cisco ISR4331  
- Switch  
- Deux PC dans des sous-réseaux différents

## Topologie  
- PC1 : 192.168.1.10/24 (réseau autorisé)  
- PC2 : 192.168.2.10/24 (réseau restreint)  
- Routeur avec deux interfaces :  
  - GigabitEthernet0/0/0 : 192.168.1.1/24  
  - GigabitEthernet0/0/1 : 192.168.2.1/24

## Étapes de configuration

```bash
enable
configure terminal

banner motd 'Ishac-LAB'

interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface GigabitEthernet0/0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

access-list 110 deny icmp host 192.168.2.10 any
access-list 110 permit ip any any

interface GigabitEthernet0/0/1
ip access-group 110 in
exit

write memory
