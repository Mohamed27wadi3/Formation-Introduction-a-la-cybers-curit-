# Module 5 : Mots de Passe et Authentification

[← Module précédent](module4-securite-web.md) | [Retour au sommaire](../README.md) | [Module suivant →](module6-ingenierie-sociale.md)

---

## 5.1 Pourquoi les Mots de Passe sont Critiques

Les mots de passe sont la première ligne de défense pour protéger vos comptes et données. Pourtant, ils restent l'un des maillons les plus faibles de la chaîne de sécurité.

### Statistiques alarmantes

- **"123456"** est le mot de passe le plus utilisé dans le monde
- **81 %** des violations de données liées au hacking impliquent des mots de passe volés ou faibles
- **65 %** des utilisateurs réutilisent le même mot de passe sur plusieurs sites
- Une attaque par force brute peut tester des **milliards de mots de passe par seconde**

---

## 5.2 Ce qui Rend un Mot de Passe Fort

### Critères d'un bon mot de passe

| Critère | Faible ❌ | Fort ✅ |
|---------|-----------|---------|
| **Longueur** | Moins de 8 caractères | 12 caractères ou plus |
| **Complexité** | Uniquement des lettres | Majuscules + minuscules + chiffres + symboles |
| **Prévisibilité** | Mots du dictionnaire | Combinaison aléatoire |
| **Unicité** | Réutilisé sur plusieurs sites | Unique par compte |
| **Informations personnelles** | Contient nom, date de naissance | Aucune info personnelle |

### Exemples

```
Mots de passe faibles ❌ :
- 123456
- password
- motdepasse
- prénom + année de naissance (alice1990)
- mot du dictionnaire (soleil)

Mots de passe forts ✅ :
- K#9mP2vL@xQr4&nB
- correct-horse-battery-staple (passphrase longue)
- 3a!Qw8$mN2#pLz7@
```

### Entropie du mot de passe

L'entropie mesure l'imprévisibilité d'un mot de passe.

```
Alphabet de 26 lettres minuscules, longueur 6 : 26^6 = 308 millions de combinaisons
Alphabet de 95 caractères, longueur 12 : 95^12 = 540 billions de billions de combinaisons
```

---

## 5.3 Attaques sur les Mots de Passe

### Attaque par Force Brute
Tester toutes les combinaisons possibles.

```
Temps pour casser un mot de passe (avec un GPU moderne) :
- 6 caractères, lettres seulement : < 1 seconde
- 8 caractères, lettres + chiffres : quelques heures
- 12 caractères, tous types : millions d'années
```

### Attaque par Dictionnaire
Tester une liste de mots courants, variantes et mots de passe connus.

### Credential Stuffing
Utiliser des identifiants volés lors de fuites de données sur d'autres services.

> **Exemple** : Votre mot de passe du site A est volé. Si vous utilisez le même sur le site B, l'attaquant peut y accéder automatiquement.

### Attaque par Table Arc-en-Ciel (Rainbow Table)
Utiliser des tables précalculées de hachages pour inverser rapidement les mots de passe hachés.

> **Contre-mesure** : Le salage (salt) ajoute une valeur aléatoire unique avant de hacher, rendant ces tables inutiles.

### Phishing de Credentials
Tromper l'utilisateur pour qu'il saisisse ses identifiants sur un faux site.

---

## 5.4 Stockage Sécurisé des Mots de Passe

### Ce qu'il ne faut pas faire

```python
# JAMAIS en clair ❌
mot_de_passe_stocké = "monMotDePasse123"

# JAMAIS en MD5 ou SHA1 (trop rapides, tables rainbow) ❌
import hashlib
hash_non_securise = hashlib.md5("monMotDePasse123".encode()).hexdigest()
```

### Ce qu'il faut faire

```python
# Bcrypt : lent intentionnellement, avec sel automatique ✅
import bcrypt
salt = bcrypt.gensalt(rounds=12)  # Plus c'est élevé, plus c'est lent
hash_securise = bcrypt.hashpw("monMotDePasse123".encode(), salt)

# Argon2 : recommandé par l'OWASP ✅
from argon2 import PasswordHasher
ph = PasswordHasher()
hash_securise = ph.hash("monMotDePasse123")
```

| Algorithme | Recommandation |
|-----------|----------------|
| **MD5** | ❌ Obsolète, ne pas utiliser |
| **SHA-1** | ❌ Obsolète, ne pas utiliser |
| **SHA-256** | ⚠️ Acceptable avec sel, mais trop rapide |
| **Bcrypt** | ✅ Recommandé |
| **Argon2** | ✅ Très recommandé (gagnant PHC 2015) |
| **scrypt** | ✅ Recommandé |

---

## 5.5 Gestionnaires de Mots de Passe

Un **gestionnaire de mots de passe** stocke et génère des mots de passe forts de manière sécurisée. Vous n'avez besoin de mémoriser qu'un seul mot de passe maître.

### Fonctionnalités

- 🔑 Génération de mots de passe forts et uniques
- 🔒 Stockage chiffré (AES-256 généralement)
- 📱 Synchronisation multi-appareils
- ⚠️ Alertes en cas de fuite de données
- 🔐 Remplissage automatique sécurisé

### Solutions populaires

| Outil | Type | Hébergement |
|-------|------|-------------|
| **Bitwarden** | Open source | Cloud ou auto-hébergé |
| **KeePassXC** | Open source | Local |
| **1Password** | Commercial | Cloud |
| **Dashlane** | Commercial | Cloud |

> 💡 **Recommandation** : Bitwarden est gratuit, open source et fortement recommandé.

---

## 5.6 Authentification Multi-Facteurs (MFA)

### Les facteurs d'authentification

| Facteur | Type | Exemples |
|---------|------|---------|
| **Ce que vous savez** | Connaissance | Mot de passe, PIN, questions secrètes |
| **Ce que vous possédez** | Possession | Smartphone, clé USB de sécurité, carte |
| **Ce que vous êtes** | Inhérence | Empreinte digitale, reconnaissance faciale |

La **MFA** (ou 2FA pour deux facteurs) combine au moins deux facteurs différents.

### Types de MFA

| Type | Sécurité | Facilité | Description |
|------|----------|----------|-------------|
| **SMS** | ⚠️ Faible | Très facile | Code par SMS (vulnérable au SIM swapping) |
| **Application TOTP** | ✅ Bonne | Facile | Google Authenticator, Authy |
| **Clé matérielle** | ✅✅ Excellente | Modérée | YubiKey, clé FIDO2 |
| **Notification push** | ✅ Bonne | Facile | Duo Security, Microsoft Authenticator |

### Comment fonctionne TOTP

```
TOTP (Time-based One-Time Password) :
1. Lors de la configuration : partage d'un secret entre serveur et app
2. Lors de la connexion :
   - L'app génère un code à 6 chiffres basé sur le secret + l'heure actuelle
   - Le code change toutes les 30 secondes
   - Le serveur génère le même code et vérifie la correspondance
```

> ⚠️ Les codes SMS (2FA par SMS) sont vulnérables au **SIM swapping** : un attaquant peut transférer votre numéro vers sa carte SIM. Préférez une application TOTP ou une clé matérielle.

---

## 5.7 Bonnes Pratiques

### Pour les utilisateurs

```
✅ Utiliser un gestionnaire de mots de passe
✅ Activer la MFA partout où c'est possible
✅ Utiliser un mot de passe unique par service
✅ Ne jamais partager ses mots de passe
✅ Vérifier ses fuites sur haveibeenpwned.com
✅ Changer les mots de passe compromis immédiatement
❌ Ne jamais noter les mots de passe sur papier ou en clair
❌ Ne jamais utiliser des informations personnelles
❌ Ne jamais utiliser le même mot de passe sur plusieurs sites
```

### Pour les entreprises

- Imposer des politiques de mots de passe (longueur, complexité, expiration)
- Implémenter la MFA pour tous les accès
- Former les employés sur les bonnes pratiques
- Surveiller les accès inhabituels
- Mettre en place le SSO (Single Sign-On) avec un fournisseur d'identité sécurisé

---

## 5.8 Quiz - Module 5

**Question 1** : Quel algorithme est recommandé pour hacher les mots de passe ?
- A) MD5
- B) SHA-1
- C) Argon2 ✅
- D) Base64

**Question 2** : Qu'est-ce que l'authentification multi-facteurs ?
- A) Utiliser plusieurs mots de passe
- B) Combiner plusieurs méthodes d'authentification de types différents ✅
- C) Changer son mot de passe fréquemment
- D) Utiliser un long mot de passe

**Question 3** : Quel type de MFA est le moins sécurisé ?
- A) Clé matérielle FIDO2
- B) Application TOTP
- C) Code SMS ✅
- D) Notification push

**Question 4** : Qu'est-ce que le "credential stuffing" ?
- A) Créer des mots de passe complexes
- B) Utiliser des identifiants volés sur d'autres services ✅
- C) Tester toutes les combinaisons possibles
- D) Phishing de mots de passe

---

## Résumé du Module 5

✅ Un mot de passe fort est long, complexe, unique et sans informations personnelles

✅ Les attaques incluent force brute, dictionnaire, credential stuffing et phishing

✅ Bcrypt et Argon2 sont les algorithmes recommandés pour stocker les mots de passe

✅ Les gestionnaires de mots de passe simplifient la gestion sécurisée des identifiants

✅ La MFA renforce significativement la sécurité des comptes

✅ Préférer les applications TOTP ou clés matérielles aux SMS pour la MFA

---

[← Module précédent : Sécurité Web](module4-securite-web.md) | [Retour au sommaire](../README.md) | [Module suivant : Ingénierie Sociale →](module6-ingenierie-sociale.md)
