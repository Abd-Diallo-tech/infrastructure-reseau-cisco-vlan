# Infrastructure Réseau avec Cisco Packet Tracer

## Présentation du projet

Ce projet consiste à concevoir et simuler une infrastructure réseau d'entreprise à l'aide de **Cisco Packet Tracer**.

Il a été réalisé dans le cadre de mon apprentissage des réseaux informatiques afin de mettre en pratique plusieurs notions étudiées, notamment les **VLAN, le trunking, le routage inter-VLAN, l'adressage IPv4/IPv6, le routage statique et l'administration des équipements**.

L'infrastructure représente une organisation composée de plusieurs services. Chaque service est séparé dans un VLAN afin de mieux organiser le réseau.

Le réseau est construit autour d'un **commutateur de niveau 3 (`switchL3`)**, relié à plusieurs commutateurs de niveau 2 et à une partie routée composée de deux routeurs.

---

## Objectifs

Les principaux objectifs de ce projet sont :

- concevoir une topologie réseau ;
- organiser le réseau avec des VLAN ;
- configurer des ports access ;
- configurer des liaisons trunk ;
- mettre en place le routage inter-VLAN ;
- configurer un plan d'adressage IPv4 ;
- mettre en pratique IPv6 ;
- configurer des routes statiques ;
- mettre en place une configuration de base pour l'administration distante ;
- vérifier la connectivité entre les différents équipements.

---

## Architecture du réseau

Le cœur du réseau est constitué d'un commutateur de niveau 3 :

- `switchL3`

Il est relié à cinq commutateurs de niveau 2 :

- `Switch-Dir-Exam`
- `Switch-Paie-Emp`
- `Med-Assu`
- `Info`
- `Switch-VPN`

Deux routeurs complètent l'infrastructure :

- `RouterCG`
- `RouterVPN`

### Topologie

![Topologie du réseau](images/topologie.png)

> La topologie a été réalisée entièrement dans Cisco Packet Tracer.

---

## Organisation des VLAN

Les différents services sont séparés à l'aide de VLAN.

| VLAN | Nom | Utilisation | Réseau IPv4 | Passerelle |
|------|-----|-------------|-------------|------------|
| 20 | Direction | Direction | `192.168.20.0/24` | `192.168.20.254` |
| 21 | Examen | Examen / Concours | `192.168.21.0/24` | `192.168.21.254` |
| 22 | Paie/DRH | Paie / Ressources humaines | `192.168.22.0/24` | `192.168.22.254` |
| 23 | Emploi | Gestion des emplois | `192.168.23.0/24` | `192.168.23.254` |
| 24 | Médecine | Service Médecine | `192.168.24.0/24` | `192.168.24.254` |
| 25 | Assurance | Service Assurance | `192.168.25.0/24` | `192.168.25.254` |
| 27 | Info | Service Information | `192.168.27.0/24` | `192.168.27.254` |
| 30 | Serveurs | Réseau des serveurs | `192.168.30.0/24` | `192.168.30.254` |
| 40 | Impression | Imprimantes réseau | `192.168.40.0/24` | `192.168.40.254` |
| 50 | Téléphonie | Téléphonie IP | `192.168.50.0/24` | `192.168.50.254` |
| 60 | Wi-Fi | Réseau sans fil | `192.168.60.0/24` | `192.168.60.254` |
| 100 | Administration | Gestion des équipements | `192.168.100.0/24` | `192.168.100.254` |

Cette organisation permet de séparer les différents services au niveau du réseau.

---

## Commutateurs de niveau 2

### Switch-Dir-Exam

Ce commutateur est utilisé pour les services **Direction** et **Examen/Concours**.

Les VLAN principaux utilisés sont :

- VLAN 20 : Direction
- VLAN 21 : Examen
- VLAN 40 : Impression
- VLAN 50 : Téléphonie
- VLAN 100 : Administration

### Switch-Paie-Emp

Ce commutateur est utilisé pour :

- VLAN 22 : Paie/DRH
- VLAN 23 : Emploi
- VLAN 40 : Impression
- VLAN 50 : Téléphonie
- VLAN 100 : Administration

### Med-Assu

Ce commutateur regroupe les services :

- Médecine
- Assurance

Il participe également à la gestion des réseaux communs comme l'impression, la téléphonie et l'administration.

### Info

Ce commutateur est utilisé pour le service Information.

Il est également intégré au réseau d'administration.

### Switch-VPN

Ce commutateur est utilisé pour la partie VPN de l'infrastructure et permet de connecter les équipements associés à cette partie du réseau.

---

## Commutation et VLAN

Les ports connectés aux équipements finaux sont configurés en mode **access**.

Exemple :

```text
interface FastEthernet0/1
 switchport access vlan 20
 switchport mode access