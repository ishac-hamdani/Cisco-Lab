# Lab13_NAT
## Objectif
Implémenter un NAT avec surcharge (PAT) entre un réseau local (LAN) et l’extérieur.

## 🛠️ Architecture Réseau

L'architecture du lab NAT/PAT est composée des éléments suivants :

```
[PC0] --- [Switch] --- [R1] --- [Cloud/Internet]
             |           |
       IP: 192.168.1.X   |-- Gi0/1: 192.168.1.1 (NAT inside)
                         |-- Gi0/0: 200.1.1.1   (NAT outside)
```

- **PC0** : Client dans le réseau LAN, reçoit son IP via DHCP.
- **R1** : Routeur NAT, réalise la traduction d’adresses (NAT/PAT).
- **Cloud ou Server PT** : Sert de destination simulée pour les tests Internet.
- **DHCP activé** sur R1 pour attribuer une IP automatiquement à PC0.
- **Fichier web `helloworld.html`** hébergé sur le serveur pour test HTTP.

PC1 :
- DHCP automatique depuis R1

R1 :

-  G0/0 → vers le serveur (NAT outside) – IP : 200.1.1.1/8

-  G0/1 → vers le LAN (NAT inside) – IP : 192.168.1.1/24

- Server PT : héberge helloworld.html

## Configuration
```bash
enable
configure terminal
hostname R1
interface GigabitEthernet0/0
 ip address 200.1.1.1 255.0.0.0
 ip nat outside
exit

interface GigabitEthernet0/1
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
exit

! DHCP
ip dhcp excluded-address 192.168.1.1
ip dhcp pool LAN1
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1

! NAT
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface GigabitEthernet0/0 overload
exit 
banner motd ^CIshac-LAB^C
end
write memory
```
