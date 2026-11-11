# Règles de contribution — Zêblè OS v0.1

## Objet

Ce document définit les règles de contribution, de documentation, de tests et de revue pour le projet Zêblè OS.

## Statut

Ce document est à l'état v0.1 (cadrage initial). Il pourra évoluer avec le projet.

## 1. Qui peut contribuer

Toute personne peut proposer des contributions. Le fondateur conserve l'autorité finale sur l'acceptation ou le refus de toute modification.

## 2. Types de contributions

### Contributions documentaires ordinaires

- Création ou modification de documents de cadrage, d'architecture, de roadmap, de gouvernance.
- Correction de fautes, d'erreurs factuelles, d'incohérences dans la documentation existante.
- Ajout de liens internes entre documents.

Ces contributions peuvent être réalisées dans le cadre de la mission initiale sans validation supplémentaire, sous réserve du respect des règles de ce document.

### Contributions sensibles

Les opérations suivantes nécessitent une **proposition détaillée et une autorisation explicite du fondateur** avant toute exécution :

1. Modification du noyau.
2. Modification du bootloader.
3. Modification des mécanismes de sécurité.
4. Désactivation d'une protection de sécurité.
5. Modification du chiffrement.
6. Modification des mécanismes OTA.
7. Ajout de dépendances payantes.
8. Choix d'une licence définitive.
9. Publication d'une version présentée comme fonctionnelle.

Toute proposition de contribution sensible doit inclure :

1. Objectif.
2. État actuel.
3. Modification envisagée.
4. Justification.
5. Avantages.
6. Risques.
7. Alternatives.
8. Procédure de retour arrière.

Le silence du fondateur ne vaut pas autorisation.

## 3. Processus de soumission

1. Créer une branche dédiée à partir de `main` ou de la branche de développement en cours.
2. Y apporter les modifications documentaires ou de code.
3. Vérifier que aucun fichier sensible ou configuration existante n'a été modifié involontairement.
4. Créer un commit descriptif et explicite.
5. Ouvrir une Pull Request vers `main`.
6. Ne jamais fusionner automatiquement. La fusion nécessite l'approbation du fondateur ou de l'architecture supervision.

## 4. Règles de documentation

- Chaque document doit indiquer sa version (ex: v0.1) et son statut (brouillon, proposé, approuvé, obsolète).
- Toute exigence doit posséder un identifiant unique (ex: EX-001).
- Toute exigence doit posséder un moyen de vérification identifié.
- Toute décision technique doit posséder un statut.
- Aucun résultat de test non exécuté ne doit être déclaré réussi.
- Les liens internes entre documents doivent être vérifiés avant toute demande de fusion.

## 5. Règles de revue

- Toute Pull Request doit être revue par au moins une personne autre que l'auteur.
- Les modifications sensibles nécessitent l'approbation explicite du fondateur.
- Une Pull Request ne peut être fusionnée tant que tous les commentaires de revue n'ont pas été résolus.

## 6. Tests et vérification

- Toute commande de test ou de vérification doit être documentée (commande utilisée, résultat réel, statut réussi/échec/non exécuté).
- Les erreurs doivent être classifiées : configuration, dépendance, permission, réseau, compilation, logique, sécurité.
- Aucune correction non autorisée ne doit être appliquée.

## 7. Licence des contributions

En contribuant, chaque contributeur accepte que ses contributions soient soumises à la licence définitive choisie par le fondateur (voir `docs/licences/LICENSE-DECISION.md`).