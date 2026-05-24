# CCNA Day 9 - Switch Interfaces : Cours & Lab

Ce dépôt regroupe les notes théoriques et la documentation technique du laboratoire pratique associé au **Day 9** du cursus CCNA (Jeremy's IT Lab), centré sur la configuration des interfaces de commutateurs, la négociation de vitesse/duplex et la gestion des erreurs.

---

## 📘 1. Notes de Cours (Théorie)

### A. Domaines de collision et CSMA/CD
* **LAN Hub (Concentrateur) :** Tous les équipements connectés à un hub font partie d'un seul et même domaine de collision. Deux appareils ne peuvent pas envoyer un paquet en même temps.
* **CSMA/CD (Carrier Sense Multiple Access with Collision Detection) :**
  * **Écoute :** Les appareils écoutent le média avant d'émettre pour vérifier qu'il est libre.
  * **Collision :** Si deux appareils émettent en même temps, ils envoient un signal de brouillage (*jamming signal*).
  * **Attente :** Chaque appareil attend un délai aléatoire avant de tenter une nouvelle transmission.

### B. Mode Duplex (Half vs Full)
* **Half Duplex :** Transmission bidirectionnelle non simultanée. L'appareil ne peut pas envoyer et recevoir des données en même temps (cas typique des hubs).
* **Full Duplex :** Transmission bidirectionnelle simultanée. L'appareil envoie et reçoit des données en même temps (cas typique des commutateurs).

### C. Vitesse et Auto-négociation
* **Paramètres par défaut :** Les interfaces utilisent généralement `speed auto` et `duplex auto` pour négocier les meilleures performances possibles avec le voisin.
* **Duplex Mismatch (Asymétrie) :** Si un côté est configuré manuellement en Full Duplex et que l'autre côté négocie en Half Duplex, des collisions et des pertes de performances massives se produiront sur la liaison.

### D. Erreurs d'Interfaces
La commande `show interfaces` permet d'analyser les différents compteurs d'erreurs d'une interface :
* **Runts :** Trames inférieures à la taille minimale autorisée (64 octets).
* **Giants :** Trames supérieures à la taille maximale autorisée (1518 octets).
* **CRC :** Trames ayant échoué au contrôle d'intégrité dans le trailer FCS.
* **Frame :** Trames reçues avec un format incorrect ou incomplet.
* **Input errors :** Somme globale de toutes les erreurs reçues en entrée.
* **Output errors :** Nombre de trames que le switch a échoué à envoyer.

---

## 🛠 2. Guide du Laboratoire Pratique

### A. Présentation de la Topologie
Le réseau global est configuré sur l'espace d'adressage **`172.16.0.0/16`**.

* **Routeur R1 :** Passerelle configurée avec l'adresse `172.16.255.254`.
* **Switch 1 (SW1) :** Connecté à R1 via `G0/1`, à PC1 (`172.16.0.1`) via `F0/1` et à PC2 (`172.16.0.2`) via `F0/2`.
* **Switch 2 (SW2) :** Connecté à R1 via `G0/2`, à PC3 (`172.16.0.3`) via `F0/1` et à PC4 (`172.16.0.4`) via `F0/2`.

### B. Configuration de SW1
Voici les commandes appliquées sur le commutateur SW1 pour forcer les paramètres de l'interface montante et sécuriser l'architecture :

```ios
SW1> enable
SW1# configure terminal

# Configuration du port GigabitEthernet connecté au routeur R1
SW1(config)# interface g0/1
SW1(config-if)# speed 1000
SW1(config-if)# duplex full
SW1(config-if)# description ## to R1 ##
SW1(config-if)# exit

# Désactivation en masse des ports inutilisés pour des raisons de sécurité
SW1(config)# interface range g0/2 , f0/3 - 22
SW1(config-if-range)# shutdown
SW1(config-if-range)# end

# Sauvegarde de la configuration
SW1# write memory
```

> **Note de configuration :** Le fait de forcer manuellement la vitesse et le duplex permet d'éviter les pannes liées aux défauts d'auto-négociation. L'utilisation de la commande `interface range` optimise l'application des configurations de sécurité.

### C. Configuration des Hôtes (Exemple PC4)
* **Adresse IP :** `172.16.0.4`
* **Masque de sous-réseau :** `255.255.0.0`
* **Passerelle par défaut :** `172.16.255.254`

### D. Commandes de Vérification
Pour valider le bon fonctionnement et l'état des commutateurs, utilisez les commandes de diagnostic suivantes :

* `show interface status` : Affiche un tableau récapitulatif synthétique (Statut, VLAN, Duplex réel ou auto, Vitesse réelle ou auto).
* `show interfaces f0/1` : Affiche les compteurs détaillés d'une interface spécifique, incluant l'adresse MAC d'usine (BIA) et les erreurs d'interface.
* `show ip interface brief` : Permet une vérification rapide de l'état logique et physique (`Up/Up`) de l'ensemble des ports.

