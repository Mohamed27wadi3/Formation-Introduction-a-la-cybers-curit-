# Module 7 : Réponse aux Incidents et Bonnes Pratiques

[← Module précédent](module6-ingenierie-sociale.md) | [Retour au sommaire](../README.md) | [Glossaire →](glossaire.md)

---

## 7.1 Qu'est-ce qu'un Incident de Sécurité ?

Un **incident de sécurité** est tout événement qui compromet ou menace la confidentialité, l'intégrité ou la disponibilité des systèmes d'information.

### Exemples d'incidents

- Infection par un ransomware
- Violation de données (fuite d'informations)
- Accès non autorisé à un système
- Déni de service (DDoS)
- Perte ou vol d'un appareil contenant des données sensibles
- Compromission d'un compte utilisateur
- Défacement d'un site web

### Différence entre événement et incident

```
Événement de sécurité : toute activité observable sur un système
    Exemple : Une connexion échouée

Incident de sécurité : événement ayant un impact négatif réel ou potentiel
    Exemple : 10 000 connexions échouées en 1 minute → attaque par force brute
```

---

## 7.2 Le Cycle de Réponse aux Incidents (PICERL)

La réponse aux incidents suit un cycle structuré. Le cadre **PICERL** (NIST) est largement adopté :

```
     ┌─────────────┐
     │ Préparation │ ←──────────────────────────────────┐
     └──────┬──────┘                                    │
            ↓                                           │
     ┌─────────────────┐                                │
     │ Identification  │                                │
     └──────┬──────────┘                                │
            ↓                                           │
     ┌─────────────────┐                       ┌────────┴──────────┐
     │   Confinement   │                       │  Leçons apprises  │
     └──────┬──────────┘                       └────────┬──────────┘
            ↓                                           ↑
     ┌─────────────────┐                       ┌────────┴──────────┐
     │   Eradication   │                       │   Récupération    │
     └──────┬──────────┘                       └───────────────────┘
            └──────────────────────────────────────────┘
```

### Phase 1 : Préparation

Mettre en place les outils, processus et équipes avant qu'un incident survienne.

- ✅ Constituer une équipe de réponse aux incidents (CSIRT)
- ✅ Documenter les procédures de réponse
- ✅ Maintenir un inventaire des actifs
- ✅ Mettre en place des outils de surveillance (SIEM, IDS)
- ✅ Effectuer des sauvegardes régulières testées
- ✅ Former les équipes

### Phase 2 : Identification

Détecter et confirmer l'incident.

- Analyser les alertes et logs
- Déterminer la portée de l'incident
- Classer la sévérité
- Documenter toutes les observations

**Sources de détection** :
```
→ Alertes SIEM
→ Alertes antivirus/EDR
→ Rapports d'utilisateurs
→ Surveillance réseau (IDS/IPS)
→ Surveillance des performances (pic inhabituel)
→ Notification externe (CERT, partenaires)
```

### Phase 3 : Confinement

Limiter la propagation de l'incident.

**Confinement à court terme** :
- Isoler les systèmes compromis du réseau
- Bloquer les adresses IP malveillantes
- Désactiver les comptes compromis

**Confinement à long terme** :
- Appliquer des correctifs temporaires
- Surveiller les systèmes adjacents

> ⚠️ Conserver des preuves avant de modifier les systèmes (forensique).

### Phase 4 : Éradication

Éliminer la cause racine de l'incident.

- Supprimer les malwares
- Corriger les vulnérabilités exploitées
- Changer les mots de passe compromis
- Mettre à jour les systèmes affectés

### Phase 5 : Récupération

Restaurer les systèmes à leur état normal.

- Restaurer depuis des sauvegardes propres
- Surveiller intensivement les systèmes restaurés
- Vérifier que tout fonctionne normalement
- Retirer progressivement les mesures de confinement

### Phase 6 : Leçons Apprises

Analyser l'incident pour s'améliorer.

- Rédiger un rapport post-incident (post-mortem)
- Identifier ce qui a fonctionné et ce qui a échoué
- Mettre à jour les procédures et outils
- Former les équipes sur les nouvelles menaces identifiées

---

## 7.3 Le Plan de Continuité d'Activité (PCA/PRA)

### PCA (Plan de Continuité d'Activité)
Maintenir les activités critiques pendant et après un incident.

### PRA (Plan de Reprise d'Activité)
Restaurer les systèmes et reprendre les activités normales après un incident.

### Indicateurs clés

| Indicateur | Définition |
|-----------|------------|
| **RTO** (Recovery Time Objective) | Durée maximale d'interruption acceptable |
| **RPO** (Recovery Point Objective) | Perte de données maximale acceptable |
| **MTTR** (Mean Time To Recover) | Temps moyen de récupération |
| **MTBF** (Mean Time Between Failures) | Temps moyen entre les pannes |

---

## 7.4 Les Sauvegardes - Règle du 3-2-1

La **règle 3-2-1** est la norme pour une stratégie de sauvegarde robuste :

```
3 copies des données
  2 sur des supports différents
    1 hors site (ou dans le cloud)

Exemple :
- 1 copie sur le serveur de production
- 1 copie sur un disque externe dans l'entreprise
- 1 copie dans le cloud ou dans un autre bâtiment
```

### Bonnes pratiques de sauvegarde

- ✅ Automatiser les sauvegardes régulières
- ✅ Tester la restauration périodiquement
- ✅ Chiffrer les sauvegardes
- ✅ Protéger les sauvegardes contre les ransomwares (air gap)
- ✅ Documenter les procédures de restauration

---

## 7.5 Surveillance et Détection

### SIEM (Security Information and Event Management)
Centralise et corrèle les logs de sécurité de tous les systèmes pour détecter les menaces.

```
Sources de logs → SIEM → Corrélation → Alertes → Analyste SOC
    ↑
Serveurs, pare-feux, antivirus, applications, équipements réseau...
```

### SOC (Security Operations Center)
Équipe dédiée à la surveillance 24/7 de la sécurité de l'organisation.

### Threat Intelligence
Informations sur les menaces actuelles pour anticiper et prévenir les attaques.

---

## 7.6 Obligations Légales en Cas d'Incident

### RGPD - Notification obligatoire

En cas de violation de données personnelles :

```
72 heures : Notifier la CNIL (en France) si la violation présente un risque
→ Pour les personnes concernées : si le risque est élevé, les notifier sans délai

Que contient la notification à la CNIL ?
- Nature de la violation
- Catégories et nombre de personnes concernées
- Mesures prises ou envisagées
- Coordonnées du DPO
```

### Signalement aux autorités

- **ANSSI** : pour les opérateurs d'importance vitale et les opérateurs de services essentiels
- **Cybermalveillance.gouv.fr** : pour les PME, collectivités et particuliers
- **Police/Gendarmerie** : pour déposer plainte

---

## 7.7 Bonnes Pratiques Générales

### Hygiène numérique au quotidien

```
Mises à jour :
☑ Mettre à jour le système d'exploitation régulièrement
☑ Mettre à jour les applications et navigateurs
☑ Mettre à jour les firmwares des équipements
☑ Supprimer les logiciels non utilisés

Comptes et accès :
☑ Utiliser des mots de passe forts et uniques (gestionnaire)
☑ Activer la MFA sur tous les comptes importants
☑ Principe du moindre privilège (donner seulement les droits nécessaires)
☑ Révoquer les accès des personnes qui quittent l'organisation

Appareils :
☑ Chiffrer les disques durs (BitLocker, FileVault)
☑ Verrouiller l'écran automatiquement
☑ Utiliser un antivirus/EDR à jour
☑ Activer le pare-feu local

Données :
☑ Sauvegardes régulières (règle 3-2-1)
☑ Chiffrer les données sensibles
☑ Supprimer définitivement les données inutiles

Navigation :
☑ Utiliser HTTPS (vérifier le cadenas)
☑ Méfiance envers les liens et pièces jointes
☑ Éviter les réseaux Wi-Fi publics (ou utiliser VPN)
☑ Utiliser un navigateur à jour avec extensions de sécurité
```

### Checklist de sécurité organisationnelle

| Domaine | Action | Priorité |
|---------|--------|----------|
| **Gouvernance** | Politique de sécurité documentée | 🔴 Haute |
| **Identités** | MFA déployé pour tous | 🔴 Haute |
| **Accès** | Principe du moindre privilège | 🔴 Haute |
| **Mises à jour** | Patch management automatisé | 🔴 Haute |
| **Sauvegardes** | Règle 3-2-1 testée | 🔴 Haute |
| **Formation** | Sensibilisation annuelle | 🟡 Moyenne |
| **Surveillance** | SIEM en place | 🟡 Moyenne |
| **Incidents** | Plan de réponse documenté | 🟡 Moyenne |
| **Tests** | Pentests annuels | 🟢 Standard |
| **Continuité** | PCA/PRA testé | 🟢 Standard |

---

## 7.8 Quiz - Module 7

**Question 1** : Que signifie l'acronyme SIEM ?
- A) Security Intelligence Event Manager
- B) Security Information and Event Management ✅
- C) System Intrusion and Event Monitor
- D) Secure Information Exchange Module

**Question 2** : Quelle est la règle de sauvegarde recommandée ?
- A) Règle 1-1-1
- B) Règle 2-2-2
- C) Règle 3-2-1 ✅
- D) Règle 4-3-2

**Question 3** : Dans le cadre PICERL, que signifie la phase "Éradication" ?
- A) Isoler les systèmes compromis
- B) Restaurer les systèmes
- C) Éliminer la cause racine de l'incident ✅
- D) Détecter et confirmer l'incident

**Question 4** : Dans quel délai faut-il notifier la CNIL en cas de violation de données (RGPD) ?
- A) 24 heures
- B) 72 heures ✅
- C) 7 jours
- D) 30 jours

---

## Résumé du Module 7

✅ Un incident de sécurité compromet la confidentialité, l'intégrité ou la disponibilité

✅ Le cycle PICERL guide la réponse aux incidents : Préparation → Identification → Confinement → Éradication → Récupération → Leçons

✅ La règle 3-2-1 garantit des sauvegardes robustes

✅ Le SIEM centralise les logs pour détecter les menaces

✅ Le RGPD impose de notifier la CNIL dans les 72h en cas de violation de données

✅ L'hygiène numérique au quotidien réduit considérablement les risques

---

## Félicitations ! 🎉

Vous avez terminé la formation **Introduction à la Cybersécurité**. Vous connaissez maintenant :

- Les fondamentaux et la triade CIA
- Les principaux types de menaces et d'attaques
- Les bases de la sécurité réseau
- Les vulnérabilités web et comment les prévenir
- Comment gérer vos mots de passe et activer la MFA
- Les techniques d'ingénierie sociale et comment s'en protéger
- Comment répondre à un incident de sécurité

### Pour aller plus loin

- 📚 **ANSSI** : [ssi.gouv.fr](https://www.ssi.gouv.fr) - Guides et recommandations
- 📚 **Cybermalveillance** : [cybermalveillance.gouv.fr](https://www.cybermalveillance.gouv.fr) - Assistance et ressources
- 🎓 **MOOC SecNum** : [secnumacademie.gouv.fr](https://secnumacademie.gouv.fr) - Formation certifiante ANSSI
- 🎓 **OWASP** : [owasp.org](https://owasp.org) - Sécurité des applications web
- 🎓 **TryHackMe** : [tryhackme.com](https://tryhackme.com) - Apprentissage pratique de la cybersécurité
- 🎓 **Hack The Box** : [hackthebox.com](https://www.hackthebox.com) - Challenges et labs avancés

---

[← Module précédent : Ingénierie Sociale](module6-ingenierie-sociale.md) | [Retour au sommaire](../README.md) | [Glossaire →](glossaire.md)
