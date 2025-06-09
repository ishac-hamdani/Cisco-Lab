# Lab02_VLANs-Isolation

## Objectif

Créer deux VLANs isolés sur un switch de niveau 2. Vérifier qu'aucune communication n'est possible entre les hôtes de VLANs différents sans routage inter-VLAN.

## Topologie

- 1 switch (Cisco 2960)
- 2 PC
- PC1 connecté à `Fa0/1` → VLAN 10 (Professeur)
- PC2 connecté à `Fa0/2` → VLAN 20 (Étudiant)

## Configuration
```bash
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name Professeur
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# name Etudiant
Switch(config-vlan)# exit
Switch(config)# interface fastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
Switch(config)# interface fastEthernet 0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit

