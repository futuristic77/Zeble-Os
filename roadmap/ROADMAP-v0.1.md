# Roadmap — Zêblè OS v0.1

## Objet

Organiser le développement en étapes réalistes.

## Statut

Proposition — en attente d'approbation par le fondateur.

## 1. Étapes de développement

| Étape | Nom | Objectif | Critère de validation | Statut |
|-------|-----|----------|----------------------|--------|
| 1 | Cadrage | Définir la vision, l'architecture, la gouvernance, les risques. | Documents v0.1 créés et révisés. | En cours (v0.1) |
| 2 | Étude de faisabilité matérielle | Identifier les smartphones économiques compatibles ARM64 avec pilotes disponibles. | Rapport de faisabilité rédigé. | Non démarré |
| 3 | Sélection d'un appareil de référence | Choisir un appareil concret pour le développement et les tests. | Appareil sélectionné et documenté. | Non démarré |
| 4 | Étude des sources et pilotes | Analyser les sources du noyau, les pilotes et le matériel de référence. | Inventaire des pilotes disponibles et manquants. | Non démarré |
| 5 | Faisabilité de compilation | Démontrer que le système peut être compilé pour l'appareil de référence. | Build réussie d'un système minimal démarrable. | Non démarré |
| 6 | Prototype d'interface | Créer une interface utilisateur originale (bété/tapa/poids akan) en français. | Prototype UI affiché sur émulateur ou matériel. | Non démarré |
| 7 | Prototype système | Assembler un système démarrant sur l'appareil de référence. | Système démarre et affiche l'interface. | Non démarré |
| 8 | Tests et validation | Tester AVB, SELinux, chiffrement, OTA, compatibilité Android. | Tous les tests de sécurité et compatibilité exécutés. | Non démarré |
| 9 | Préparation du MVP | Préparer une version minimale viable présentée comme fonctionnelle. | MVP documenté, testé, approuvé par le fondateur. | Non démarré |

## 2. Dépendances entre les étapes

```
Étape 1 (Cadrage) → Étape 2 (Faisabilité matérielle) → Étape 3 (Sélection appareil)
                                                      ↓
                                            Étape 4 (Étude sources/pilotes)
                                                      ↓
                                            Étape 5 (Faisabilité compilation)
                                                      ↓
                                            Étape 6 (Prototype UI) → Étape 7 (Prototype système)
                                                                           ↓
                                                             Étape 8 (Tests et validation)
                                                                           ↓
                                                             Étape 9 (Préparation MVP)
```

## 3. Jalons

| Jalon | Étape associée | Date cible | Statut |
|-------|---------------|------------|--------|
| JAL-001 | Cadrage terminé | v0.1 | En cours |
| JAL-002 | Appareil de référence sélectionné | Après étape 3 | Non démarré |
| JAL-003 | Système compilable | Après étape 5 | Non démarré |
| JAL-004 | Prototype système démarrant | Après étape 7 | Non démarré |
| JAL-005 | MVP prêt | Après étape 9 | Non démarré |

## 4. Risques et mesures de réduction

| Étape | Risque | Niveau | Mesure de réduction |
|-------|--------|--------|---------------------|
| 2 | Aucun appareil économique avec pilotes ouverts | Critique | Étudier plusieurs appareils avant sélection |
| 3 | Appareil devenu obsolète | Modéré | Choisir un appareil avec support à long terme |
| 5 | Échec de compilation (dépendances manquantes) | Élevé | Préparer un environnement de build documenté |
| 6 | UI trop lourde pour smartphones économiques | Modéré | Optimiser pour ressources limitées dès le prototype |
| 8 | Incompatibilité Android non résolue | Élevé | Tester la compatibilité tôt (étape 5-6) |
| 9 | MVP non approuvé par le fondateur | Modéré | Valider chaque jalon avec le fondateur |

## 5. Note importante

Aucune étape au-delà du cadrage (étape 1) n'a été commencée à ce stade. Le dépôt est vide. Aucune compilation n'a été tentée. Aucun matériel n'a été testé.