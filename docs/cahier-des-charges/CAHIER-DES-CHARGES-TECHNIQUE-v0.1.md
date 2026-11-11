# Cahier des charges technique — Zêblè OS v0.1

## 1. Vision

Créer progressivement un système d'exploitation mobile ivoirien, original, accessible et évolutif, destiné en priorité aux smartphones économiques.

## 2. Objectifs

| Objectif | Description | Priorité |
|----------|-------------|----------|
| OBJ-001 | Proposer un système d'exploitation mobile original, inspiré de la culture ivoirienne (alphabet bété, tapa, géométrie akan). | Haute |
| OBJ-002 | Cibler les smartphones économiques (contrainte matérielle forte). | Haute |
| OBJ-003 | Rechercher la compatibilité avec les applications Android. | Haute |
| OBJ-004 | Assurer une identité visuelle originale. | Moyenne |
| OBJ-005 | Langue initiale : français. | Moyenne |
| OBJ-006 | Souveraineté technologique progressive. | Long terme |
| OBJ-007 | Recherche indépendante sur l'évolution du noyau. | Long terme |

## 3. Périmètre fonctionnel

### Inclus (v0.1 - cadrage)

- Définition de l'architecture cible.
- Définition des modules et de leurs interfaces.
- Définition des mécanismes de sécurité.
- Définition de la stratégie de compatibilité Android.
- Roadmap de développement.

### Exclus (v0.1)

- Code source du système d'exploitation.
- Noyau Linux customisé.
- Pilotes matériels.
- HAL (Hardware Abstraction Layer).
- Framework applicatif.
- Interface utilisateur implémentée.
- Applications natives.
- Mécanismes OTA implémentés.
## 4. Contraintes matérielles

| Contrainte | Détail | Source |
|------------|--------|--------|
| CM-001 | Smartphones économiques (mémoire limitée, processeur d'entrée/milieu de gamme). | Décision du fondateur |
| CM-002 | Architecture ARM64 à confirmer selon le matériel sélectionné. | Orientation technique |
| CM-003 | Pas de matériel de référence sélectionné à ce stade. | Audit initial |
| CM-004 | Gestion énergétique optimisée pour l'autonomie. | Exigence non fonctionnelle |

## 5. Exigences fonctionnelles

| ID | Exigence | Moyen de vérification | Statut |
|----|----------|----------------------|--------|
| EX-001 | Le système doit pouvoir démarrer sur un appareil de référence. | Test de démarrage sur matériel | Non exécuté |
| EX-002 | Le système doit proposer une interface utilisateur en français. | Test d'affichage de l'UI | Non exécuté |
| EX-003 | Le système doit pouvoir exécuter des applications Android (compatibilité à vérifier). | Test d'installation d'APK | Non exécuté |
| EX-004 | Le système doit intégrer une identité visuelle inspirée des signes bété, du tapa et des poids akan. | Revue visuelle | Non exécuté |
| EX-005 | Le système doit assurer le chiffrement des données utilisateur. | Revue du mécanisme de chiffrement | Non exécuté |
| EX-006 | Le système doit supporter les mises à jour OTA signées. | Revue du mécanisme OTA | Non exécuté |

*Aucun des tests ci-dessus n'a été exécuté à ce stade (Phase 1 : dépôt vide).*

## 6. Exigences non fonctionnelles

| ID | Exigence | Moyen de vérification | Statut |
|----|----------|----------------------|--------|
| ENF-001 | Le système doit fonctionner sur des smartphones économiques (RAM limitée, stockage limité). | Test sur matériel cible | Non exécuté |
| ENF-002 | SELinux en mode enforcing. | Audit du noyau et de la configuration | Non exécuté |
| ENF-003 | Android Verified Boot (AVB) activé. | Test de démarrage vérifié | Non exécuté |
| ENF-004 | Protection contre le retour à une version vulnérable (rollback protection). | Test de downgrade | Non exécuté |
| ENF-005 | Mises à jour OTA signées. | Vérification de signature | Non exécuté |

*Aucun des tests ci-dessus n'a été exécuté à ce stade.*

## 7. Architecture envisagée

L'architecture est présentée dans `docs/architecture/ARCHITECTURE-CIBLE-v0.1.md`. Les couches sont :

1. Bootloader
2. Noyau Linux
3. Pilotes
4. HAL
5. Framework
6. Services système
7. Interface utilisateur
8. Applications
9. Mécanismes de sécurité et de mise à jour

**Hypothèse** : Une base AOSP est étudiée comme point de départ possible, mais son choix n'est pas encore acté.

## 8. Sécurité

| ID | Exigence | Détail | Statut |
|----|----------|--------|--------|
| SEC-001 | Android Verified Boot (AVB) | Chaîne de confiance du bootloader au noyau | Non évalué |
| SEC-002 | SELinux enforcing | Politique de confinement des processus | Non évalué |
| SEC-003 | Chiffrement des données | Chiffrement de stockage basé sur fichier | Non évalué |
| SEC-004 | Isolation des applications | Sandbox par application (UID dédié) | Non évalué |
| SEC-005 | Permissions | Modèle de permissions Android-like | Non évalué |
| SEC-006 | OTA signées | Vérification cryptographique des mises à jour | Non évalué |
| SEC-007 | Protection anti-rollback | Empêchement du retour à une version vulnérable | Non évalué |
| SEC-008 | Gestion des clés | Stockage sécurisé des clés de chiffrement et de signature | Non évalué |

*Aucune protection ne doit être désactivée pour faciliter les tests.*

## 9. Compatibilité

| Type de compatibilité | Détail | Statut |
|----------------------|--------|--------|
| Framework Android | Compatibilité avec le framework d'applications Android | À étudier |
| Applications Android | Capacité à exécuter des APK non modifiés | À vérifier par tests réels |
| Services Google (GMS) | Compatibilité avec Google Play Services, Play Store | Non acquise automatiquement |
| Play Store | Disponibilité éventuelle | Soumis à certification et licence Google |


## 10. Critères d'acceptation

| ID | Critère | Statut |
|----|---------|--------|
| CA-001 | Documentation de cadrage complète et cohérente. | En cours (v0.1) |
| CA-002 | Architecture cible définie et documentée. | En cours (v0.1) |
| CA-003 | Matériel de référence sélectionné. | Non réalisé |
| CA-004 | Faisabilité de compilation démontrée. | Non réalisé |
| CA-005 | Prototype d'interface fonctionnel. | Non réalisé |
| CA-006 | Prototype système démarrant sur matériel de référence. | Non réalisé |
| CA-007 | Tests de sécurité (AVB, SELinux, chiffrement) validés. | Non réalisé |

## 11. Risques

| ID | Risque | Niveau | Conséquence | Mesure de réduction |
|----|--------|--------|-------------|---------------------|
| RK-001 | Incompatibilité matérielle (pilotes manquants). | Critique | Échec du démarrage sur l'appareil de référence | Sélection précoce d'un appareil avec pilotes disponibles |
| RK-002 | Incompatibilité Android (APK non exécutables). | Élevé | Perte de l'atout principal du projet | Tests réels tôt sur le framework |
| RK-003 | Licence GMS non obtenue. | Élevé | Pas de Play Store ni de services Google | Se concentrer sur le framework AOSP sans GMS |
| RK-004 | Coûts de maintenance du noyau custom. | Élevé | Dépassement budgétaire | Limiter les modifications du noyau au strict nécessaire |
| RK-005 | Obsolescence du matériel de référence. | Modéré | Ré-ingénierie nécessaire | Choisir un appareil avec support à long terme |
| RK-006 | Ressources humaines limitées. | Modéré | Ralentissement du développement | Documenter précisément pour faciliter l'onboarding |

## 12. Décisions ouvertes

| ID | Décision en attente | Date d'ouverture | Décideur |
|----|---------------------|------------------|----------|
| DO-001 | Choix de la base système (AOSP, distribution Linux mobile, autre). | v0.1 | Fondateur |
| DO-002 | Choix de l'appareil de référence. | v0.1 | Fondateur |
| DO-003 | Choix de la licence définitive. | v0.1 | Fondateur |
| DO-004 | Architecture ARM64 confirmée ou alternative. | v0.1 | Fondateur |
| DO-005 | Stratégie de compatibilité Android (framework uniquement ou incl. GMS). | v0.1 | Fondateur |

## 13. Matrice de traçabilité (exigences → modules → validation)

| ID Exigence | Module responsable | Méthode de validation | Statut |
|-------------|-------------------|----------------------|--------|
| EX-001 | Bootloader + Noyau | Test de démarrage matériel | Non exécuté |
| EX-002 | Interface utilisateur | Revue visuelle | Non exécuté |
| EX-003 | Framework Android + HAL | Test d'installation APK | Non exécuté |
| EX-004 | Interface utilisateur | Revue visuelle | Non exécuté |
| EX-005 | Sécurité (chiffrement) | Audit du mécanisme | Non exécuté |
| EX-006 | Services système (OTA) | Vérification de signature | Non exécuté |
| ENF-001 | Toutes les couches | Test sur matériel cible | Non exécuté |
| ENF-002 | Noyau + SELinux | Audit configuration | Non exécuté |
| ENF-003 | Bootloader + AVB | Test démarrage vérifié | Non exécuté |
| ENF-004 | Services système (OTA) | Test de downgrade | Non exécuté |
| ENF-005 | Services système (OTA) | Vérification de signature | Non exécuté |
| SEC-001 à SEC-008 | Sécurité + Noyau + Services | Audit de sécurité complet | Non exécuté |

*L'ensemble de cette matrice est à l'état initial (v0.1). Aucun test n'a encore été exécuté.*
**Avertissement** : La compatibilité GMS n'est pas automatiquement acquise avec AOSP. Elle nécessite des accords de licence et de certification avec Google.