# Décision de licence — Zêblè OS v0.1

## Objet

Présenter les possibilités de licences et leurs implications pour le projet Zêblè OS.

## Règle de gouvernance

**Aucune licence globale n'est choisie à ce stade.** Le choix d'une licence définitive nécessite une approbation explicite du fondateur (voir `docs/GOUVERNANCE.md` et `CONTRIBUTING.md`).

## 1. Contexte

Le projet Zêblè OS est un système d'exploitation mobile. Selon la base système choisie (AOSP, distribution Linux mobile, ou développement from-scratch), différentes contraintes de licence s'appliqueront.

## 2. Options de licence envisagées

| Licence | Type | Implications | Compatibilité AOSP | Adapté à Zêblè OS ? |
|---------|------|--------------|--------------------|---------------------|
| Apache 2.0 | Permissive | Permet l'utilisation, la modification, la distribution. Exige la conservation des mentions de licence et des avis de brevet. | Oui (AOSP utilise principalement Apache 2.0 et BSD) | Possible |
| MIT | Permissive | Très permissive, exige seulement la conservation de la notice de copyright. | Oui | Possible |
| BSD (2 ou 3 clauses) | Permissive | Similaire à MIT, avec ou sans clause de non-endossement. | Oui | Possible |
| GPL v2 | Copyleft | Exige que les œuvres dérivées soient sous la même licence. | Partiel (noyau Linux est GPL v2) | Possible mais contraignant |
| GPL v3 | Copyleft fort | GPL v2 + protection contre les brevets, anti-tivoization. | Non recommandé avec AOSP | Déconseillé |
| AGPL v3 | Copyleft réseau | GPL v3 + obligation de publier le code si utilisé en tant que service. | Non compatible avec AOSP | Non recommandé |
| Licence propriétaire | Fermée | Contrôle total du fondateur, pas de partage du code source obligatoire. | Non compatible avec AOSP | Contredit la transparence |

## 3. Contraintes liées à la base système

### Si AOSP est choisi

- Le noyau Linux est sous GPL v2.
- La plupart du userland Android est sous Apache 2.0.
- Certaines bibliothèques sont sous BSD, MIT, LGPL.
- **Conséquence** : Toute distribution basée sur AOSP doit respecter la GPL v2 pour le noyau (code source disponible sur demande) et Apache 2.0 pour le reste.

### Si une distribution Linux mobile est choisie (ex: PostmarketOS, Mobian, etc.)

- Dépend de la distribution (souvent GPL v2/v3, LGPL, MIT).
- **Conséquence** : Respect des licences de la distribution et de ses paquets.

### Si développement from-scratch

- Liberté totale de choix de licence.
- **Conséquence** : Réécriture complète de tous les composants (noyau, pilotes, HAL, framework, UI), coût très élevé.

## 4. Implications pour le projet Zêblè OS

| Aspect | Implication |
|--------|-------------|
| Code source | Si GPL v2 est présent (noyau Linux), le code source du noyau modifié doit être disponible. |
| Modifications | Les modifications du noyau Linux doivent être redistribuées sous GPL v2. |
| Applications tierces | Les applications développées par des tiers peuvent être sous n'importe quelle licence (si l'OS est sous licence permissive). |
| Commercialisation | Sous Apache 2.0/MIT/BSD : possible de créer des versions propriétaires dérivées. Sous GPL : les dérivés doivent rester libres. |
| Brevets | Apache 2.0 inclut une licence de brevet implicite. |

## 5. Recommandations (non décision)

- **Licence permissive (Apache 2.0 ou MIT)** : adaptée si le fondateur souhaite maximiser l'adoption, permettre des dérivés propriétaires, et rester compatible avec AOSP.
- **Copyleft (GPL v2)** : adapté si le fondateur souhaite s'assurer que toutes les modifications du noyau restent libres et disponibles.

Ces recommandations ne constituent pas une décision. Le fondateur doit choisir.

## 6. Décisions ouvertes

| ID | Question | Statut | Décideur |
|----|----------|--------|----------|
| DO-003 | Choix de la licence définitive pour Zêblè OS. | Ouvert | Fondateur |
| DO-011 | Licence pour les applications natives développées par l'équipe Zêblè. | Ouvert | Fondateur |
| DO-012 | Politique de contribution (CLA, DCO, ou aucune). | Ouvert | Fondateur |

## 7. Prochaine étape

Le fondateur doit se prononcer sur le choix de la licence avant toute publication de code ou de version présentée comme fonctionnelle.