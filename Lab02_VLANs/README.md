# Lab02_VLANs

## Description
Topologie avec deux VLANs configurés sur deux switches de couche 2 et routage inter-VLAN réalisé via un routeur (router-on-a-stick).

## VLANs
- VLAN 10 : PC1 connecté au port assigné sur Switch1 (Layer 3)
- VLAN 20 : PC2 connecté au port assigné sur Switch2 (Layer 3)

## Configuration des switches
- Création des VLANs 10 et 20
- Attribution des ports aux VLANs respectifs en mode access
- Configuration du trunk entre les switches et vers le routeur

## Routage inter-VLAN
- Configuration d’une interface sub-interface sur le routeur pour chaque VLAN
- Assignation d’adresses IP aux interfaces sub-interfaces
- Activation du routage inter-VLAN sur le routeur

## Vérification
- Tester la communication entre PC1 et PC2 (doit réussir grâce au routage inter-VLAN)
- Tester la communication entre chaque PC et son interface VLAN respective

## Fichiers
- `Lab02_VLANs.pkt` : topologie Packet Tracer
- `configs/` : configurations CLI des switches et routeur

## Instructions d’usage
1. Ouvrir le fichier Packet Tracer
2. Charger les configurations dans les équipements ou configurer manuellement selon les fichiers `configs/`
3. Vérifier la connectivité entre les VLANs via les PCs
