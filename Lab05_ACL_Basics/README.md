# Lab05_ACL_Basics - Listes de contrôle d'accès sur routeur Cisco

## Objectif  
Configurer des ACL (Access Control List) pour filtrer le trafic réseau selon des adresses IP ou des services.

## Matériel  
- Routeur Cisco  
- Switch  
- PC connectés dans différents sous-réseaux  

## Topologie  
- PC1 (réseau interne, ex: 192.168.1.0/24)  
- PC2 (réseau externe, ex: 192.168.2.0/24)  
- Routeur reliant les deux réseaux  

## Étapes de configuration

```bash
enable
configure terminal

access-list 10 deny 192.168.1.100
access-list 10 permit any

interface FastEthernet0/0
ip access-group 10 in

exit
write memory
