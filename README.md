# Conception et Déploiement d’une Infrastructure Réseau Multisites Segmentée

**Auteur :** Adam SAHMI  
**Encadrant :** Prof. Azeddine KHIAT  
**Module :** Réseaux Informatiques  
**Outil :** Cisco Packet Tracer

---

## 📖 Description du Projet

Ce projet consiste en la conception et le déploiement simulé d'une infrastructure réseau d'entreprise multisite robuste et sécurisée. L'objectif principal est de répondre aux besoins organisationnels modernes en assurant la performance, la sécurité et la haute disponibilité des services.

L'architecture repose sur trois sites géographiques (un siège central et deux sites distants) interconnectés via un réseau WAN simulé.

## 🎯 Objectifs Techniques

Le projet met en œuvre les technologies réseaux fondamentales suivantes :

* **Segmentation Logique (VLANs) :** Isolation des flux pour améliorer la sécurité et la gestion.
* **Haute Disponibilité (Switching) :** Agrégation de liens avec **EtherChannel (LACP)** pour la redondance et la performance.
* **Routage Inter-VLAN :** Utilisation de l'architecture **Router-on-a-Stick** sur le routeur central.
* **Interconnexion WAN :** Configuration du **Routage Statique** pour relier le siège aux sites distants.
* **Validation :** Tests de connectivité (Ping, Traceroute) et analyse des tables de routage.

## 🏗️ Architecture et Topologie

L'infrastructure est divisée en trois zones :
1.  **Siège Central :** Comprend deux switchs (S1, S2) en couche d'accès et un routeur (R1).
2.  **Sites Distants :** Deux sites annexes gérés par les routeurs R2 et R3.
3.  **Liaisons WAN :** Connexions série point-à-point.

*(Insérez ici une capture d'écran de votre topologie Packet Tracer, par exemple : `![Topologie Réseau](images/topologie.png)`) - Optionnel*

## 📊 Plan d'Adressage et VLANs

### VLANs du Site Principal
| VLAN | Nom | Adresse Réseau | Masque | Passerelle (R1) |
| :--- | :--- | :--- | :--- | :--- |
| **10** | Utilisateurs 1 | 172.18.10.0 | /28 (255.255.255.240) | 172.18.10.14 |
| **20** | Utilisateurs 2 | 172.18.20.0 | /28 (255.255.255.240) | 172.18.20.14 |
| **30** | Utilisateurs 3 | 172.18.30.0 | /28 (255.255.255.240) | 172.18.30.14 |
| **50** | Native (Sécurité) | 172.18.50.0 | /28 (255.255.255.240) | 172.18.50.14 |
| **60** | Gestion/Admin | 172.18.60.0 | /28 (255.255.255.240) | 172.18.60.14 |

### Adressage WAN (Inter-Routeurs)
* **R1 – R2 :** 10.0.30.176 /30
* **R1 – R3 :** 10.0.30.180 /30
* **R2 – R3 :** 10.0.30.184 /30

## ⚙️ Configuration et Fonctionnalités Clés

### 1. Switching (Couche 2)
* Création et affectation des VLANs.
* Configuration des ports en mode **Access** pour les utilisateurs.
* Mise en place de **Trunks 802.1Q** avec VLAN Natif 50 sécurisé.
* Agrégation de liens **EtherChannel** (Groupe 1, mode Active LACP) entre S1 et S2.

### 2. Routage (Couche 3)
* **R1 (Router-on-a-Stick) :** Création de sous-interfaces (ex: `Fa0/0.10`) pour le routage entre les VLANs.
* **Routage Statique :** Configuration des routes sur R1 pour atteindre les réseaux distants et routes par défaut sur R2/R3 vers le siège.

## ✅ Tests et Validation

Le projet a été validé par les tests suivants :
* [x] **Ping Inter-VLAN :** Succès de la communication entre VLAN 10 et VLAN 20.
* [x] **Traceroute WAN :** Validation du chemin complet du siège vers les sites distants (Saut R1 -> Saut WAN -> Destination).
* [x] **Gestion :** Accès aux interfaces de gestion des switchs.

## 🚀 Comment utiliser ce projet

1.  Clonez ce dépôt.
2.  Ouvrez le fichier `.pkt` (Project source) avec **Cisco Packet Tracer**.
3.  Utilisez l'onglet "Simulation" ou "Real-time" pour tester les Pings entre les PC.

---
