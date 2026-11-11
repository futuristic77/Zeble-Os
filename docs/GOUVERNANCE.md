# Gouvernance — Zêblè OS v0.1

## Objet

Définir les responsabilités, le contrôle des modifications et les règles d'approbation pour le projet Zêblè OS.

## 1. Rôles et responsabilités

### Fondateur (autorité finale)

Le fondateur est le propriétaire du projet. Il conserve l'autorité finale sur :

- La vision et les orientations stratégiques.
- Le choix de la base système (AOSP, distribution Linux mobile, autre).
- Le choix de l'architecture matérielle.
- Le choix de la licence définitive.
- Toute publication présentée comme fonctionnelle.
- Toute modification sensible (noyau, bootloader, sécurité, chiffrement, OTA, dépendances payantes).

### Responsable de l'architecture et de la supervision (ChatGPT, en collaboration avec le fondateur)

- Analyse technique et justification des choix.
- Rédaction et maintenance de la documentation technique.
- Évaluation des risques et des alternatives.
- Supervision du processus de revue et de validation.

### Agent d'exécution (Cline)

- Observation de l'existant et audit initial.
- Création de la documentation conformément au cahier des charges.
- Préparation des branches, commits et Pull Requests.
- Exécution des vérifications documentaires disponibles.
- Jamais de fusion automatique.

### Contributeurs externes

- Soumission de propositions via Pull Request.
- Respect des règles de contribution (`CONTRIBUTING.md`).
- Aucune autorité de décision sur les orientations stratégiques.

## 2. Contrôle des modifications

### Modifications ordinaires (documentation de cadrage)

Peuvent être réalisées par l'agent d'exécution sans validation supplémentaire, sous réserve :

- De ne pas modifier de fichier sensible ou de configuration existante.
- De respecter la structure documentaire définie.
- De documenter chaque changement dans le message de commit.

### Modifications sensibles (requièrent autorisation explicite du fondateur)

- Modification du noyau.
- Modification du bootloader.
- Modification des mécanismes de sécurité.
- Désactivation d'une protection.
- Modification du chiffrement.
- Modification des mécanismes OTA.
- Ajout de dépendances payantes.
- Choix d'une licence définitive.
- Publication d'une version présentée comme fonctionnelle.

### Procédure pour une modification sensible

1. Présentation d'une proposition détaillée (8 points : objectif, état actuel, modification envisagée, justification, avantages, risques, alternatives, procédure de retour arrière).
2. Attente du feu vert explicite du fondateur.
3. Exécution uniquement après autorisation.
4. Enregistrement de l'autorisation dans le journal des décisions.

## 3. Règles d'approbation

- Toute décision technique doit avoir un statut explicite : `proposé`, `en études`, `approuvé`, `rejeté`, `obsolète`.
- Toute approbation doit être consignée par écrit (commit, issue, ou document dédié).
- Le silence ne vaut jamais approbation.
- Les décisions approuvées sont consignées dans `docs/decisions-techniques/`.

## 4. Journal des décisions

Les décisions approuvées sont consignées dans le fichier `docs/decisions-techniques/README.md` avec :

- Identifiant de la décision (ex: DEC-001).
- Date.
- Décision.
- Justification.
- Autorité ayant approuvé.
- Statut.

## 5. Conflits d'intérêts

Aucun contributeur ne peut approuver sa propre modification sensible. Toute décision sensible nécessite l'approbation du fondateur.

## 6. Évolution de la gouvernance

Ce document pourra évoluer avec le projet. Toute modification de la gouvernance nécessite l'approbation du fondateur.