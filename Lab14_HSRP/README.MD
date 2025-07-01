# LAB14_HSRP

## Objectif  
Mettre en place une redondance de passerelle avec **HSRP** (Hot Standby Router Protocol) pour assurer la haute disponibilité du réseau.

## Architecture Réseau

L'architecture du lab HSRP est composée des éléments suivants :

[PC0] --- [Switch] --- [R1]
| |
| |-- Gi0/0: 192.168.1.2 (HSRP)
|
---- [R2]
|
|-- Gi0/0: 192.168.1.3 (HSRP)

- **PC0** : Client dans le réseau LAN, utilise l’IP virtuelle HSRP comme passerelle.
- **R1** : Routeur actif avec priorité plus élevée.
- **R2** : Routeur de secours (standby).
- **HSRP** : Fournit une IP virtuelle (`192.168.1.1`) comme passerelle commune.
- **Failover automatique** en cas de défaillance de **R1**.

## Configuration

### R1
```bash
enable
configure terminal
hostname R1
interface GigabitEthernet0/0
 ip address 192.168.1.2 255.255.255.0
 standby 1 ip 192.168.1.1
 standby 1 priority 110
 standby 1 preempt
 no shutdown
exit
banner motd ^CR1 - HSRP Actif^C
end
write memory
```

### R1
```bash
enable
configure terminal
hostname R2
interface GigabitEthernet0/0
 ip address 192.168.1.3 255.255.255.0
 standby 1 ip 192.168.1.1
 standby 1 priority 100
 standby 1 preempt
 no shutdown
exit
banner motd ^CR2 - HSRP Standby^C
end
write memory
```
