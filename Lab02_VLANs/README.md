# Lab02_VLANs-Isolation

## Objectif  
Configurer deux VLANs isolés sur un switch Cisco de niveau 2. Vérifier qu'aucune communication n’est possible entre les hôtes appartenant à des VLANs différents sans routage inter-VLAN.

## Matériel  
- Switch Cisco Layer 2 (ex. Catalyst 2960)  
- 2 PC connectés en mode accès  
- VLAN 10 (Professeur), VLAN 20 (Étudiant)

## Topologie  
- PC1 connecté à `Fa0/1` → VLAN 10 (Professeur)  
- PC2 connecté à `Fa0/2` → VLAN 20 (Étudiant)

## Configuration principale  
- Création des VLANs  
- Affectation des ports en mode accès aux VLANs  
- Vérification de l’isolation entre les VLANs

## Commandes principales  
```bash
enable
configure terminal

vlan 10
name Professeur
exit

vlan 20
name Etudiant
exit

interface fastEthernet 0/1
switchport mode access
switchport access vlan 10
exit

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20
exit

end
write memory
```
## Configuration PC ##
PC VLAN 10 : IP 192.168.10.10 /24, passerelle vide
PC VLAN 20 : IP 192.168.20.10 /24, passerelle vide

## Tests ##
Ping entre les deux PC → échec attendu (pas de routage inter-VLAN)
