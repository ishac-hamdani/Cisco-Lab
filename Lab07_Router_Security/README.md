# Lab07_Router_Security - Sécurité du routeur (SSH, authentification locale, pare-feu basique)

## Objectif  
Sécuriser l’accès à un routeur Cisco dans Packet Tracer :  
- Activer l’accès SSH uniquement  
- Utiliser une base locale pour l’authentification  
- Configurer un pare-feu basique via des ACL  

## Matériel  
- Routeur Cisco ISR4331  
- Switch  
- PC pour les tests d'accès (Telnet/SSH/ping)

## Topologie  
- Routeur connecté au switch via GigabitEthernet0/0/0  
- PC connecté au switch  
- Réseau : 192.168.1.0/24  
- IP routeur : 192.168.1.1  
- IP PC : 192.168.1.10  

## Étapes de configuration  
```bash
enable
configure terminal

hostname R1
ip domain-name ishac.local
banner motd 'Ishac-LAB'

username admin privilege 15 secret cisco123

crypto key generate rsa
# Choisir une taille de clé >= 1024

ip ssh version 2
line vty 0 4
 transport input ssh
 login local
 exit

interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

ip access-list standard FIREWALL
 deny 192.168.1.50
 permit any

interface GigabitEthernet0/0/0
 ip access-group FIREWALL in
exit

write memory
```

## Explications
-username crée un utilisateur local pour SSH.
-crypto key generate rsa active SSH.
-login local force l’authentification par le compte local.
-transport input ssh bloque Telnet.
-ACL FIREWALL bloque une IP précise (ex. 192.168.1.50).
-ip access-group applique l’ACL au trafic entrant.

## Tests
Depuis le PC :
-Tester SSH vers 192.168.1.1 → accès demandé avec login/password
-Tester Telnet → refusé
-Simuler un PC avec IP 192.168.1.50 → bloqué par l’ACL
