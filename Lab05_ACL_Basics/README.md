# Lab05_ACL_Basics - Blocage ICMP selon l'adresse IP

## Objectif  
Configurer une ACL pour empêcher un PC spécifique (PC2) de faire des requêtes ICMP (ping), tout en laissant un autre PC (PC1) communiquer normalement.

## Matériel  
- Routeur Cisco  
- Switch  
- Deux PC dans des sous-réseaux différents

## Topologie  
- PC1 : 192.168.1.10/24 (réseau autorisé)
- PC2 : 192.168.2.10/24 (réseau restreint)
- Routeur avec deux interfaces :
  - Fa0/0 : 192.168.1.1/24
  - Fa0/1 : 192.168.2.1/24

## Étapes de configuration

```bash
enable
configure terminal

access-list 110 deny icmp host 192.168.2.10 any
access-list 110 permit ip any any

interface FastEthernet0/1
ip access-group 110 in

exit
write memory
