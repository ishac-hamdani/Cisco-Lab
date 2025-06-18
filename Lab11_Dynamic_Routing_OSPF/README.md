# Lab – Routage Dynamique avec OSPF (Multi-area)

## Objectif  
Configurer un réseau avec plusieurs routeurs qui échangent automatiquement leurs routes grâce à OSPF. Chaque routeur gère un LAN avec des clients utilisant DHCP pour obtenir leur adresse IP.

## C’est quoi OSPF ?
OSPF (Open Shortest Path First) est un protocole de routage dynamique qui permet aux routeurs de partager leurs informations de réseau pour construire automatiquement une table de routage optimale. Il divise le réseau en « areas » (zones) pour mieux gérer la complexité et améliorer la performance.

## Pourquoi utiliser OSPF ?
Automatisation du routage : plus besoin de configurer manuellement chaque route.
Adaptation rapide aux changements du réseau (ex : panne d’un lien).
Supporte de grandes topologies avec plusieurs zones (multi-area).

## Topologie
R0 : routeur backbone.
R1 à R4 : chaque routeur a un LAN avec un pool DHCP.
Les routeurs sont connectés entre eux par des liens séries.
Les liens et LANs sont répartis dans différentes areas OSPF.

## Vérifications
Les PC obtiennent bien une IP via DHCP.
Ping possible entre les différents LANs.
Vérifier les routes apprises et adjacences OSPF sur chaque routeur.
