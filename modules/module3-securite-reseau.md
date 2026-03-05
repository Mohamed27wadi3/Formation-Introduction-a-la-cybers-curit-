# Module 3 : Sécurité Réseau

[← Module précédent](module2-menaces-et-attaques.md) | [Retour au sommaire](../README.md) | [Module suivant →](module4-securite-web.md)

---

## 3.1 Fondamentaux des Réseaux

Avant d'aborder la sécurité réseau, il est important de comprendre les bases des réseaux informatiques.

### Le Modèle OSI (7 couches)

| Couche | Nom | Rôle | Exemples de protocoles |
|--------|-----|------|----------------------|
| 7 | Application | Interface avec l'utilisateur | HTTP, SMTP, FTP, DNS |
| 6 | Présentation | Chiffrement, compression | SSL/TLS, JPEG |
| 5 | Session | Gestion des sessions | NetBIOS, RPC |
| 4 | Transport | Transmission fiable | TCP, UDP |
| 3 | Réseau | Routage | IP, ICMP, ARP |
| 2 | Liaison de données | Transmission locale | Ethernet, Wi-Fi |
| 1 | Physique | Transmission des bits | Câbles, ondes radio |

### Protocoles Importants

**TCP/IP** : Protocole fondamental d'Internet
- **TCP** (Transmission Control Protocol) : fiable, avec vérification des erreurs
- **UDP** (User Datagram Protocol) : rapide, sans garantie de livraison

**DNS** (Domain Name System) : traduit les noms de domaine en adresses IP
```
Navigateur → "www.exemple.com" → Serveur DNS → "93.184.216.34" → Serveur web
```

**HTTP/HTTPS** : protocoles de communication web
- HTTP : non chiffré (à éviter)
- HTTPS : chiffré via TLS (à privilégier)

---

## 3.2 Pare-feu (Firewall)

Un **pare-feu** est un dispositif de sécurité qui contrôle le trafic réseau entrant et sortant selon des règles prédéfinies.

### Types de pare-feu

| Type | Description | Avantages | Inconvénients |
|------|-------------|-----------|---------------|
| **Filtrage de paquets** | Analyse les en-têtes des paquets | Simple, rapide | Pas d'inspection du contenu |
| **Stateful** | Suit l'état des connexions | Plus intelligent | Plus coûteux en ressources |
| **Proxy / Application** | Analyse le contenu applicatif | Très précis | Lent, complexe |
| **NGFW** (Next Generation) | Combine toutes les techniques + IA | Très complet | Coûteux |

### Règles de pare-feu - Exemple

```
Politique par défaut : TOUT BLOQUER

Règles autorisées :
✅ Port 80 (HTTP) entrant depuis Internet
✅ Port 443 (HTTPS) entrant depuis Internet
✅ Port 22 (SSH) entrant depuis IP de l'administrateur uniquement
❌ Tout autre trafic entrant
✅ Tout trafic sortant vers Internet (sauf liste noire)
```

---

## 3.3 VPN (Virtual Private Network)

Un **VPN** crée un tunnel chiffré entre l'utilisateur et un serveur distant, protégeant les communications sur les réseaux non sécurisés.

```
Sans VPN :
Utilisateur ——(données en clair)——→ Internet ——→ Serveur

Avec VPN :
Utilisateur ——[données chiffrées]——→ Serveur VPN ——→ Internet ——→ Serveur
              ←————————tunnel sécurisé————————→
```

### Cas d'usage

- Accès distant sécurisé au réseau de l'entreprise
- Protection sur les Wi-Fi publics
- Confidentialité de la navigation

### Protocoles VPN courants

| Protocole | Sécurité | Vitesse | Usage |
|-----------|----------|---------|-------|
| **OpenVPN** | Élevée | Moyenne | Entreprises |
| **WireGuard** | Très élevée | Très rapide | Moderne, recommandé |
| **IKEv2/IPSec** | Élevée | Rapide | Mobile |
| **L2TP/IPSec** | Moyenne | Moyenne | Héritage |

---

## 3.4 IDS et IPS

### IDS (Intrusion Detection System)
Surveille le trafic réseau et **alerte** en cas d'activité suspecte.

### IPS (Intrusion Prevention System)
Surveille le trafic et **bloque** automatiquement les menaces détectées.

```
IDS : Trafic → Analyse → ALERTE (pas d'action automatique)
IPS : Trafic → Analyse → BLOCAGE AUTOMATIQUE
```

### Types de détection

- **Basée sur les signatures** : compare avec une base de menaces connues (rapide, mais ne détecte pas les nouvelles menaces)
- **Basée sur les anomalies** : détecte les comportements inhabituels (détecte les nouvelles menaces, mais plus de faux positifs)

---

## 3.5 Segmentation Réseau

Diviser le réseau en zones isolées pour limiter la propagation des attaques.

### DMZ (Zone Démilitarisée)

```
Internet
    |
[Pare-feu externe]
    |
   DMZ (Serveurs web, mail, DNS)
    |
[Pare-feu interne]
    |
Réseau interne (serveurs de données, postes de travail)
```

### VLAN (Virtual LAN)
Segmentation logique du réseau :
- VLAN RH : ressources humaines isolées
- VLAN Finance : comptabilité isolée
- VLAN Informatique : équipe IT avec plus d'accès
- VLAN Invités : Wi-Fi visiteurs sans accès au réseau interne

**Principe** : Si un appareil est compromis dans un VLAN, l'attaquant ne peut pas facilement atteindre les autres VLAN.

---

## 3.6 Chiffrement des Communications

### TLS/SSL
Protocole qui chiffre les communications sur Internet.

```
Négociation TLS (Handshake) :
1. Client → "Bonjour, je supporte TLS 1.3"
2. Serveur → "Voici mon certificat et ma clé publique"
3. Client → Vérifie le certificat, génère une clé de session
4. Les deux parties → Chiffrement de toutes les communications
```

### HTTP vs HTTPS
- **HTTP** : données en clair, vulnérable aux écoutes
- **HTTPS** = HTTP + TLS : données chiffrées

> 🔒 Toujours vérifier le cadenas dans la barre d'adresse avant de saisir des informations sensibles.

### Certificats numériques
Un certificat SSL/TLS prouve l'identité d'un site web :
- Émis par une **Autorité de Certification (CA)** de confiance
- Contient la clé publique du site
- A une date d'expiration

---

## 3.7 Sécurité Wi-Fi

### Protocoles de chiffrement Wi-Fi

| Protocole | Sécurité | Recommandation |
|-----------|----------|----------------|
| **WEP** | Très faible (cassable en minutes) | ❌ Ne pas utiliser |
| **WPA** | Faible | ❌ Ne pas utiliser |
| **WPA2** | Bonne | ⚠️ Acceptable |
| **WPA3** | Très bonne | ✅ Recommandé |

### Bonnes pratiques Wi-Fi

- Utiliser WPA3 ou WPA2 avec un mot de passe fort
- Changer le mot de passe par défaut du routeur
- Activer un réseau invité séparé
- Désactiver le WPS (vulnérable aux attaques par force brute)
- Éviter les réseaux Wi-Fi publics non chiffrés ou utiliser un VPN

---

## 3.8 Quiz - Module 3

**Question 1** : Quel outil bloque ou autorise le trafic réseau selon des règles ?
- A) Antivirus
- B) Pare-feu ✅
- C) VPN
- D) IDS

**Question 2** : Quelle est la différence principale entre IDS et IPS ?
- A) L'IPS chiffre les données, l'IDS non
- B) L'IDS alerte, l'IPS bloque automatiquement ✅
- C) L'IDS est hardware, l'IPS est software
- D) Aucune différence

**Question 3** : Quel protocole Wi-Fi est recommandé aujourd'hui ?
- A) WEP
- B) WPA
- C) WPA2
- D) WPA3 ✅

**Question 4** : Que signifie DMZ dans le contexte réseau ?
- A) Domain Management Zone
- B) Demilitarized Zone ✅
- C) Data Management Zone
- D) Digital Media Zone

---

## Résumé du Module 3

✅ Le modèle OSI comprend 7 couches, chacune avec des protocoles spécifiques

✅ Les pare-feu filtrent le trafic réseau selon des règles de sécurité

✅ Les VPN chiffrent les communications pour protéger la confidentialité

✅ Les IDS alertent et les IPS bloquent les intrusions détectées

✅ La segmentation réseau (DMZ, VLAN) limite la propagation des attaques

✅ TLS/HTTPS chiffre les communications web ; WPA3 sécurise le Wi-Fi

---

[← Module précédent : Menaces et Attaques](module2-menaces-et-attaques.md) | [Retour au sommaire](../README.md) | [Module suivant : Sécurité Web →](module4-securite-web.md)
