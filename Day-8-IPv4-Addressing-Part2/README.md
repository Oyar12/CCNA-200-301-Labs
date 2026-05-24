# CCNA Day 8 - IPv4 Addressing (Part 2) : Cours & Lab

Ce dépôt regroupe les notes théoriques du cours ainsi que la documentation technique du laboratoire pratique associé au **Day 8** du cursus CCNA.

---

## 📘 1. Notes de Cours (Théorie)

### A. Calcul du nombre de machines (Maximum Hosts per Network)
Pour déterminer le nombre d'adresses IP attribuables à des hôtes (machines, routeurs, serveurs) dans un réseau ou un sous-réseau, on utilise la formule suivante :

$$\text{Nombre d'hôtes maximum} = 2^n - 2$$

* **$n$** : Nombre de bits réservés à la partie hôte (*host bits*).
* **Pourquoi $- 2$ ?**
  1. On soustrait la première adresse (où tous les bits d'hôte sont à `0`), qui correspond à l'**adresse réseau** (*Network ID*).
  2. On soustrait la dernière adresse (mise à `1`), qui correspond à l'**adresse de diffusion** (*Broadcast address*).

**Exemple d'application :**
Pour le réseau `192.168.1.0/24` :
* Le masque `/24` signifie que 24 bits sont pour le réseau et $32 - 24 = 8$ bits sont pour les hôtes ($n = 8$).
* Partie hôte totale : $2^8 = 256$ combinaisons.
* Hôtes utilisables : $2^8 - 2 = 254$ adresses valides (de `.1` à `.254`).

### B. Analyse de la commande `show ip interface brief`
Cette commande fondamentale permet de vérifier l'état des interfaces d'un équipement Cisco. Les deux colonnes d'état font référence aux couches du modèle OSI :

1. **Status (Couche 1 - Physique) :** Indique si le câble est branché, fonctionnel, ou si l'interface est éteinte logiciellement (`administratively down`).
2. **Protocol (Couche 2 - Liaison de données) :** Indique si l'encapsulation et le protocole de liaison (comme Ethernet) sont fonctionnels.

> **Note :** Pour qu'une interface soit pleinement opérationnelle, elle doit afficher l'état **Up / Up**.

---

## 🛠 2. Guide du Laboratoire Pratique

### A. Présentation de la Topologie
Le laboratoire est réalisé sur **Cisco Packet Tracer** et met en œuvre le routage inter-réseaux via un routeur central interconnectant trois architectures distinctes :

* **Réseau Local 1 (LAN Bleu) :** Sous-réseau `15.0.0.0/8`
  * Passerelle (R1 G0/0) : `15.255.255.254`
  * Hôte terminal (PC1) : `15.0.0.1`
* **Réseau Local 2 (LAN Vert) :** Sous-réseau `182.98.0.0/16`
  * Passerelle (R1 G0/1) : `182.98.255.254`
  * Hôte terminal (PC2) : `182.98.0.1`
* **Réseau Local 3 (LAN Jaune) :** Sous-réseau `201.191.20.0/24`
  * Passerelle (R1 G0/2) : `201.191.20.254`
  * Hôte terminal (PC3) : `201.191.20.1`

### B. Script de Configuration de R1
Voici l'ensemble des commandes appliquées sur le CLI du routeur pour configurer les interfaces et documenter la topologie :

```ios
# Passage en mode privilégié et configuration globale
Router> enable
Router# configure terminal
Router(config)# hostname R1

# Configuration de l'interface GigabitEthernet 0/0 (LAN 1)
R1(config)# interface gigabitethernet 0/0
R1(config-if)# ip address 15.255.255.254 255.0.0.0
R1(config-if)# description to SW1
R1(config-if)# no shutdown
R1(config-if)# exit

# Configuration de l'interface GigabitEthernet 0/1 (LAN 2)
R1(config)# interface g0/1
R1(config-if)# ip address 182.98.255.254 255.255.0.0
R1(config-if)# description to SW2
R1(config-if)# no shutdown
R1(config-if)# exit

# Configuration de l'interface GigabitEthernet 0/2 (LAN 3)
R1(config)# interface g0/2
R1(config-if)# ip address 201.191.20.254 255.255.255.0
R1(config-if)# description to SW3
R1(config-if)# no shutdown
R1(config-if)# exit

# Sauvegarde de la configuration en cours
R1(config-if)# do write memory
```

### C. Commandes de Vérification
Pour valider l'état du routeur, les commandes de diagnostic suivantes ont été exécutées :

**Vérification abrégée des adresses et statuts :**
```ios
R1# show ip interface brief
```
* **Résultat attendu :** Les interfaces `GigabitEthernet0/0`, `0/1` et `0/2` doivent afficher le statut `up` et le protocole `up`.

**Vérification des descriptions d'interfaces :**
```ios
R1# show interfaces description
```
* **Résultat attendu :** Permet de s'assurer que chaque interface est correctement documentée vers son switch respectif (`to SW1`, `to SW2`, `to SW3`).

---

## 📸 3. Validation et Résultats

### Configuration des ordinateurs
Les adresses de PC1, PC2 et PC3 ont été attribuées statiquement dans Packet Tracer (`Desktop > IP Configuration`) en veillant à renseigner l'IP du routeur comme **Default Gateway**.

### Tests de connectivité (Ping)
Depuis l'invite de commande de PC1, des requêtes ICMP ont été envoyées vers les autres sous-réseaux :

* `ping 182.98.0.1` (PC2) ➡️ **Succès** (Le premier paquet peut expirer le temps de la résolution ARP, puis les suivants répondent avec un TTL de 127).
* `ping 201.191.20.1` (PC3) ➡️ **Succès**.

Le routage entre les trois sous-réseaux est pleinement opérationnel.
<img width="1920" height="1080" alt="Screenshot_20260519_220325" src="https://github.com/user-attachments/assets/6320383d-2282-4ddb-a2f9-8f85209a793e" />
<img width="1920" height="1080" alt="Screenshot_20260519_220218" src="https://github.com/user-attachments/assets/233e734f-2ac4-4fcb-baaf-72d7e13d383f" />
<img width="1920" height="1080" alt="Screenshot_20260519_220024" src="https://github.com/user-attachments/assets/62bb800a-a496-4f1b-b10a-dde167443c1f" />
<img width="576" height="1280" alt="jpeg" src="https://github.com/user-attachments/assets/d11136f8-9667-435c-8161-4f71118addec" />

<img width="1920" height="1080" alt="Screenshot_20260519_220024" src="https://github.com/user-attachments/assets/a0da78b8-081f-4b04-9bff-1c1f229bff85" />
