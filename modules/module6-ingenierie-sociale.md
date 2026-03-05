# Module 6 : Ingénierie Sociale

[← Module précédent](module5-mots-de-passe.md) | [Retour au sommaire](../README.md) | [Module suivant →](module7-reponse-incidents.md)

---

## 6.1 Qu'est-ce que l'Ingénierie Sociale ?

L'**ingénierie sociale** (social engineering) désigne l'ensemble des techniques de manipulation psychologique utilisées pour tromper des individus et les amener à divulguer des informations confidentielles ou à effectuer des actions non sécurisées.

> *"Il est plus facile de tromper une personne que de contourner un système informatique sécurisé."*

L'attaquant exploite des failles humaines plutôt que des vulnérabilités techniques :
- La confiance
- La peur
- L'urgence
- L'autorité
- La curiosité
- Le désir d'aider

**Statistique clé** : 95 % des cyberattaques réussies impliquent une forme d'ingénierie sociale.

---

## 6.2 Le Phishing

Le **phishing** (hameçonnage) est la technique d'ingénierie sociale la plus répandue. L'attaquant envoie un message frauduleux imitant une entité légitime pour voler des informations ou installer un malware.

### Types de phishing

| Type | Canal | Cible | Sophistication |
|------|-------|-------|----------------|
| **Phishing** | Email | Masse | Faible |
| **Spear phishing** | Email | Individu ciblé | Élevée |
| **Whaling** | Email | Dirigeants (PDG, CFO) | Très élevée |
| **Smishing** | SMS | Masse | Faible à moyenne |
| **Vishing** | Téléphone | Individus | Moyenne |
| **Quishing** | QR Code | Masse | Faible à moyenne |

### Anatomie d'un email de phishing

```
De : support@banque-france-secure.com          ← Domaine suspect (pas la vraie banque)
Objet : ⚠️ URGENT - Votre compte a été suspendu  ← Urgence artificielle

Bonjour,

Votre compte bancaire a été temporairement suspendu suite  ← Alarme
à une activité suspecte. Veuillez confirmer vos informations
dans les 24 heures pour éviter la fermeture définitive.     ← Délai de pression

[Cliquer ici pour vérifier votre compte]                    ← Lien malveillant
                        ↑
         https://banque-france-secure.com/login
         (faux site copiant la vraie banque)

Cordialement,
Service Sécurité Banque                                     ← Signature vague
```

### Signaux d'alerte d'un phishing

```
🚩 Expéditeur inconnu ou domaine suspect
🚩 Fautes d'orthographe et de grammaire
🚩 Ton urgent ou alarmiste
🚩 Demande d'informations sensibles
🚩 Liens ou pièces jointes inattendus
🚩 URL différente de l'organisation officielle
🚩 Mise en page ou logo légèrement différent
🚩 Adresse de réponse différente de l'expéditeur
```

---

## 6.3 Autres Techniques d'Ingénierie Sociale

### Pretexting (Prétextage)
Création d'un scénario fictif pour obtenir des informations ou un accès.

> **Exemple** : Un attaquant se fait passer pour un technicien informatique et appelle un employé : *"Bonjour, je suis du support IT. Nous avons détecté un problème sur votre compte. Pouvez-vous me confirmer votre mot de passe ?"*

### Baiting (Appâtage)
Laisser un support physique infecté dans l'espoir que quelqu'un le connecte.

> **Exemple** : Des clés USB infectées abandonnées sur le parking d'une entreprise. Un employé curieux la branche sur son ordinateur, déclenchant l'installation d'un malware.

### Tailgating (Filature)
Suivre discrètement une personne autorisée pour accéder physiquement à une zone sécurisée.

> **Exemple** : Un attaquant attend qu'un employé ouvre une porte sécurisée et se faufile derrière lui.

### Quid Pro Quo
Offrir un service en échange d'informations.

> **Exemple** : *"Je peux résoudre votre problème informatique, mais j'ai besoin de vos identifiants pour accéder à votre système."*

### Vishing (Voice Phishing)
Appel téléphonique frauduleux imitant une entité de confiance.

> **Exemple** : Faux appel de la "banque" signalant une transaction frauduleuse et demandant la confirmation du code de carte bancaire.

---

## 6.4 Manipulation Psychologique - Les Leviers

Les attaquants exploitent des biais cognitifs bien connus :

| Levier | Description | Exemple d'exploitation |
|--------|-------------|------------------------|
| **Autorité** | Obéir à une figure d'autorité | Se faire passer pour un manager ou la police |
| **Urgence** | Créer une pression temporelle | "Votre compte sera supprimé dans 2 heures" |
| **Peur** | Menacer de conséquences | "Vous avez un virus, appelez immédiatement" |
| **Réciprocité** | Donner quelque chose d'abord | Offrir une aide puis demander une faveur |
| **Sympathie** | Établir un lien affectif | Se lier d'amitié avant de demander quelque chose |
| **Preuve sociale** | "Tout le monde le fait" | "Vos collègues ont déjà validé, vous pouvez aussi" |
| **Rareté** | Limiter la disponibilité | "Offre valable seulement aujourd'hui" |

---

## 6.5 Comment Se Protéger

### Pour les individus

```
Vérification :
☑ Ne jamais cliquer sur des liens dans des emails suspects
☑ Taper directement l'URL officielle dans le navigateur
☑ Vérifier l'adresse email de l'expéditeur
☑ Passer la souris sur les liens avant de cliquer (hover)
☑ Appeler directement l'organisation via un numéro officiel pour confirmer

Comportement :
☑ Ne jamais communiquer des mots de passe, même à l'"IT"
☑ Méfiance envers toute demande urgente ou inhabituelle
☑ Signaler les tentatives de phishing à son équipe IT
☑ Ne pas brancher de clés USB inconnues
☑ Verrouiller son écran en quittant son poste

Technique :
☑ Activer la MFA sur tous les comptes importants
☑ Utiliser un filtre anti-phishing dans le navigateur
☑ Maintenir son système et ses logiciels à jour
```

### Pour les organisations

- **Formation régulière** des employés sur les techniques d'ingénierie sociale
- **Tests de phishing simulés** pour évaluer la vigilance
- **Processus de vérification** pour les demandes inhabituelles
- **Politique de confiance zéro** (Zero Trust)
- **Signalement facile** des tentatives suspectes

---

## 6.6 Reconnaître et Réagir à une Attaque

### Étapes en cas de phishing reçu

```
1. NE PAS cliquer sur les liens ou pièces jointes
2. NE PAS répondre à l'email
3. Signaler à votre équipe de sécurité informatique
4. Supprimer l'email
5. Si vous avez cliqué :
   → Déconnecter l'appareil du réseau
   → Contacter immédiatement l'IT
   → Changer les mots de passe compromis
   → Activer la MFA si ce n'est pas déjà fait
```

### Outils de vérification

- **VirusTotal** (virustotal.com) : analyser un URL ou fichier suspect
- **URLVoid** (urlvoid.com) : vérifier la réputation d'un URL
- **HaveIBeenPwned** (haveibeenpwned.com) : vérifier si votre email a été compromis
- **PhishTank** (phishtank.com) : base de données de sites de phishing connus

---

## 6.7 Quiz - Module 6

**Question 1** : Qu'est-ce que le "spear phishing" ?
- A) Du phishing envoyé massivement
- B) Du phishing ciblant un individu spécifique ✅
- C) Du phishing par SMS
- D) Du phishing par téléphone

**Question 2** : Qu'est-ce que le "baiting" ?
- A) Un appel téléphonique frauduleux
- B) Se faire passer pour quelqu'un d'autre
- C) Laisser un support physique infecté pour attirer la curiosité ✅
- D) Suivre quelqu'un dans une zone sécurisée

**Question 3** : Quel levier psychologique consiste à créer une pression temporelle ?
- A) Autorité
- B) Sympathie
- C) Urgence ✅
- D) Réciprocité

**Question 4** : Que faire si vous recevez un email vous demandant votre mot de passe ?
- A) Fournir le mot de passe si l'expéditeur semble légitime
- B) Répondre pour obtenir plus d'informations
- C) Ne jamais fournir votre mot de passe et signaler l'email ✅
- D) Transférer l'email à vos collègues

---

## Résumé du Module 6

✅ L'ingénierie sociale exploite les failles humaines plutôt que les failles techniques

✅ Le phishing est la technique la plus répandue (email, SMS, téléphone, QR code)

✅ Les attaquants exploitent l'autorité, l'urgence, la peur, la sympathie et la curiosité

✅ Vérifier l'expéditeur, les liens et les demandes inhabituelles avant d'agir

✅ Ne jamais communiquer son mot de passe, même à l'équipe IT

✅ La formation et les tests de phishing simulés renforcent la vigilance collective

---

[← Module précédent : Mots de Passe](module5-mots-de-passe.md) | [Retour au sommaire](../README.md) | [Module suivant : Réponse aux Incidents →](module7-reponse-incidents.md)
