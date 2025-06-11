# Lab04_Port_Security - Sécurité des ports sur switch Cisco

## Objectif  
Configurer la sécurité des ports sur un switch Cisco pour limiter les adresses MAC autorisées sur chaque port et prévenir les accès non autorisés.

## Matériel  
- Switch Cisco (Cisco Catalyst 2960)  
- PC connectés aux ports en mode accès  

## Topologie  
- Switch  
- PC1 connecté sur Fa0/1  
- PC2 connecté sur Fa0/2  

## Étapes de configuration

```bash
enable
configure terminal

interface fastEthernet 0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security violation shutdown
switchport port-security mac-address sticky
exit

interface fastEthernet 0/2
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security violation restrict
switchport port-security mac-address sticky
exit

exit
write memory
```
## Explications ##
- switchports port-security active la sécurité des ports.maximum 1 limite à une seule adresse MAC.
- violation shutdown désactive le port en cas de violation.
- violation restrict bloque le trafic non autorisé mais laisse le port actif.
- mac-address sticky apprend automatiquement l’adresse MAC connectée et la mémorise.
- Pour pouvoir refaire la manipulation il faut shutdown et no shutdown le port fastEthernet 0/1

## Tests ##
- Connecter un PC sur Fa0/1, vérifier qu’il fonctionne.
- Connecter un autre PC sur Fa0/1 : port doit se désactiver (shutdown).
- Sur Fa0/2, connecter un autre PC non autorisé : trafic bloqué mais port reste actif.
