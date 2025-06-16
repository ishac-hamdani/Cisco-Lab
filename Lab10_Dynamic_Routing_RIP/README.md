# Lab10_Dynamic_Routing_RIP – Routage Dynamique RIP entre 3 routeurs

## Objectif
# Configurer le protocole de routage RIP pour permettre la communication entre 3 réseaux LAN interconnectés via des liaisons série.

## Matériel
# - 3 routeurs Cisco (R1, R2, R3)
# - 3 switches
# - 3 PC (un par LAN)

## Topologie
# - R1 ↔ R2 ↔ R3 ↔ R1 (liaisons série formant un triangle)
# - Chaque routeur a un LAN :
#   - R1 : 192.168.1.0/24
#   - R2 : 192.168.2.0/24
#   - R3 : 192.168.3.0/24
# - Liaisons série :
#   - R1–R2 : 192.168.10.0/30
#   - R2–R3 : 192.168.20.0/30
#   - R3–R1 : 192.168.30.0/30

## Étapes de configuration (exemple R1)
enable
configure terminal

hostname R1
banner motd ^CIshac-LAB^C

interface GigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

ip dhcp excluded-address 192.168.1.1
ip dhcp pool LAN1
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
exit

interface Serial0/0/0
ip address 192.168.10.1 255.255.255.252
no shutdown
exit

interface Serial0/1/1
ip address 192.168.30.1 255.255.255.252
no shutdown
exit

router rip
version 2
no auto-summary
network 192.168.1.0
network 192.168.10.0
network 192.168.30.0
exit

write memory

## Explications
# - DHCP : attribue une IP au PC de chaque LAN.
# - RIP v2 : permet le routage dynamique entre les routeurs.
# - no auto-summary : évite le résumé de classe (utile avec les /30).
# - network : indique les réseaux directement connectés à annoncer.

## Tests
# - Vérifier que les PC obtiennent une IP via DHCP.
# - Tester la connectivité avec des pings entre tous les PC.
# - show ip route : affiche les routes RIP apprises.
# - show ip interface brief : vérifier l'état des interfaces.
