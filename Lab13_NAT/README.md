# Lab13_NAT
## Objectif
Implémenter un NAT avec surcharge (PAT) entre un réseau local (LAN) et l’extérieur.

## Architecture
[PC1] -- [SW] -- [R1] -- [Server PT]
            |       |       |
        VLAN 1   NAT    IP Publique

- PC1 : DHCP automatique depuis R1

- R1 :

-  G0/0 → vers le serveur (NAT outside) – IP : 200.1.1.1/8

-  G0/1 → vers le LAN (NAT inside) – IP : 192.168.1.1/24

- Server PT : héberge helloworld.html
