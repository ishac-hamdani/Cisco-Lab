# Lab06_DHCP_Server - Configuration d’un serveur DHCP sur un routeur Cisco

## Objectif  
Configurer un routeur Cisco pour fournir automatiquement des adresses IP aux clients via le protocole DHCP.

## Matériel  
- Routeur Cisco ISR4331  
- Switch  
- Deux PC dans le même sous-réseau  

## Topologie  
- Routeur connecté au switch via GigabitEthernet0/0/0  
- PC1 et PC2 connectés au switch  
- Réseau : 192.168.1.0/24  
- Passerelle : 192.168.1.1  
- DNS : 8.8.8.8  
- Plage DHCP : 192.168.1.11 à 192.168.1.254  
- Adresses exclues : 192.168.1.1 à 192.168.1.10  

## Étapes de configuration
```bash
enable
configure terminal

banner motd 'Ishac-LAB'

interface GigabitEthernet0/0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

ip dhcp excluded-address 192.168.1.1 192.168.1.10

ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
exit

write memory
```
## Explications
-ip dhcp excluded-address évite d’attribuer automatiquement certaines adresses (ex. pour le routeur).
-ip dhcp pool définit la plage d’adresses dynamiques.
-default-router spécifie la passerelle pour les clients.
-dns-server indique le DNS utilisé.

## Tests
-Configurer les PC en DHCP.
-Vérifier qu’ils reçoivent une IP entre 192.168.1.11 et 192.168.1.254.
-Vérifier la connectivité avec un ping vers 192.168.1.1.

