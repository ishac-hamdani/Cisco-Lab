# Lab 02 – Deux réseaux interconnectés par un routeur

## Objectif
Configurer deux réseaux différents, chacun connecté à un switch, interconnectés via un routeur. Vérifier la connectivité inter-réseaux.

## Topologie
PC0 --- SW1 --- G0/0/0 (R1) G0/0/1 --- SW2 --- PC1

## Plan d'adressage

| Appareil | Interface          | IP               | Masque           |
|----------|--------------------|------------------|------------------|
| PC0      | FastEthernet0      | 192.168.1.10     | 255.255.255.0    |
| PC1      | FastEthernet0      | 192.168.2.10     | 255.255.255.0    |
| R1       | GigabitEthernet0/0/0 | 192.168.1.1   | 255.255.255.0    |
| R1       | GigabitEthernet0/0/1 | 192.168.2.1   | 255.255.255.0    |

## Configuration du routeur
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
