# Définition des modules — Zêblè OS v0.1

## Objet

Définir les responsabilités, interfaces, dépendances et critères de validation de chaque module de l'architecture cible.

## Statut

Proposition — en attente d'approbation par le fondateur.

## 1. Modèle de description des modules

Chaque module est décrit avec :

- **Responsabilités** : ce que le module doit faire.
- **Interfaces** : ce que le module expose aux autres modules.
- **Dépendances** : ce dont le module dépend pour fonctionner.
- **Critères de validation** : comment vérifier que le module fonctionne correctement.
- **Statut** : état actuel du module (non démarré, en conception, en développement, validé, obsolète).

## 2. Modules

### 2.1 Module Bootloader (M-BL-001)

**Responsabilités** :
- Initialisation matérielle de base.
- Vérification AVB du noyau.
- Chargement du noyau.

**Interfaces** :
- Entrée : image du noyau signée.
- Sortie : exécution du noyau.

**Dépendances** :
- Matériel de référence (bootloader supporté).
- Clés de signature AVB.

**Critères de validation** :
- Démarrage réussi sur l'appareil de référence.
- Rejet d'un noyau non signé ou altéré.

**Statut** : Non démarré.

### 2.2 Module Noyau Linux (M-KRN-001)

**Responsabilités** :
- Gestion mémoire, processus, pilotes.
- SELinux en mode enforcing.
- Chiffrement du stockage.
- Protection anti-rollback.
- Gestion énergétique.

**Interfaces** :
- Appels système pour l'espace utilisateur.
- Interface de pilotes (HAL, pilotes périphériques).

**Dépendances** :
- Architecture matérielle (ARM64 à confirmer).
- Pilotes spécifiques au matériel.
- Configuration du bootloader.

**Critères de validation** :
- Compilation réussie pour l'architecture cible.
- Démarrage avec SELinux enforcing.
- Chiffrement fonctionnel.
- Rejet du rollback vers une version vulnérable.

**Statut** : Non démarré.

### 2.3 Module Pilotes (M-DRV-001 à M-DRV-009)

**Responsabilités** :
- Contrôle direct du matériel : écran, tactile, GPU, caméra, modem, Wi-Fi, Bluetooth, audio, batterie, capteurs.

**Interfaces** :
- Interface noyau (pilotes de périphérique Linux).
- Interface HAL (abstraction vers le framework).

**Dépendances** :
- Noyau Linux.
- Spécifications matérielles de l'appareil de référence.

**Critères de validation** :
- Chaque périphérique fonctionne sur l'appareil de référence.
- Aucun pilote ne cause d'instabilité du noyau.

**Statut** : Non démarré.

| Sous-module | Périphérique | Statut |
|-------------|-------------|--------|
| M-DRV-001 | Écran et tactile | Non démarré |
| M-DRV-002 | GPU | Non démarré |
| M-DRV-003 | Caméra | Non démarré |
| M-DRV-004 | Modem | Non démarré |
| M-DRV-005 | Wi-Fi | Non démarré |
| M-DRV-006 | Bluetooth | Non démarré |
| M-DRV-007 | Audio | Non démarré |
| M-DRV-008 | Gestion énergétique | Non démarré |

### 2.4 Module HAL (M-HAL-001)

**Responsabilités** :
- Abstraction des pilotes matériels.
- Interfaces standardisées pour le framework.

**Interfaces** :
- API HAL pour l'écran, le tactile, la caméra, le modem, le Wi-Fi, le Bluetooth, l'audio, l'énergie.

**Dépendances** :
- Pilotes.
- Noyau Linux.

**Critères de validation** :
- Le framework peut accéder à chaque fonctionnalité matérielle via la HAL.
- Aucune dépendance directe vers un pilote spécifique depuis le framework.

**Statut** : Non démarré.

### 2.5 Module Framework (M-FWK-001)

**Responsabilités** :
- API applicatives.
- Cycle de vie des applications.
- Gestion des ressources (fenêtres, affichage, saisie).
- Gestion des permissions.
- Intents et communication inter-applications.
- Compatibilité Android (à vérifier).

**Interfaces** :
- API pour les applications.
- Interface vers les services système.
- Interface vers la HAL.

**Dépendances** :
- HAL.
- Services système.
- Noyau Linux.

**Critères de validation** :
- Une application exemple peut s'installer et s'exécuter.
- Les permissions sont vérifiées à l'installation et à l'exécution.
- Test de compatibilité avec des APK Android (si applicable).

**Statut** : Non démarré.

### 2.6 Module Services système (M-SYS-001)

**Responsabilités** :
- Gestionnaire de paquets.
- Gestionnaire d'OTA (téléchargement, signature, installation).
- Gestion de l'énergie.
- Comptes et authentification.
- Notifications.
- Stockage et chiffrement.

**Interfaces** :
- API pour le framework et l'interface utilisateur.
- Interface OTA (serveur de mise à jour, vérification de signature).

**Dépendances** :
- Framework.
- HAL.
- Noyau Linux (chiffrement, énergie).

**Critères de validation** :
- Installation/désinstallation d'application fonctionnelle.
- Mise à jour OTA signée installée avec succès.
- Rejet d'une mise à jour non signée ou altérée.
- Chiffrement des données utilisateur fonctionnel.

**Statut** : Non démarré.

### 2.7 Module Interface utilisateur (M-UI-001)

**Responsabilités** :
- Affichage graphique.
- Gestion du tactile.
- Thème visuel original (bété, tapa, poids akan).
- Langue française.
- Accessibilité smartphones économiques.

**Interfaces** :
- API d'affichage pour les applications.
- Interface tactile.
- Interface notifications.

**Dépendances** :
- Framework.
- HAL (écran, tactile).
- Services système (notifications, comptes).

**Critères de validation** :
- Interface affichée correctement sur l'appareil de référence.
- Réponse tactile fonctionnelle.
- Thème visuel cohérent avec l'identité culturelle.
- Texte en français affiché correctement.

**Statut** : Non démarré.

### 2.8 Module Applications (M-APP-001)

**Responsabilités** :
- Applications natives Zêblè OS.
- Applications Android (si compatibilité démontrée).

**Interfaces** :
- API du framework.
- Interface utilisateur.
- Services système.

**Dépendances** :
- Framework.
- Interface utilisateur.
- Services système.

**Critères de validation** :
- Au moins une application native fonctionnelle.
- Si compatibilité Android : au moins un APK tiers s'installe et s'exécute.

**Statut** : Non démarré.

### 2.9 Module Sécurité et mise à jour (M-SEC-001)

**Responsabilités** :
- Android Verified Boot (AVB).
- SELinux en mode enforcing.
- Chiffrement des données.
- Isolation des applications.
- Permissions.
- Mises à jour OTA signées.
- Protection anti-rollback.
- Gestion des clés.

**Interfaces** :
- Interface AVB avec le bootloader.
- Interface SELinux avec le noyau.
- Interface chiffrement avec le noyau et les services système.
- Interface OTA avec les services système.

**Dépendances** :
- Bootloader.
- Noyau Linux.
- Services système (OTA).
- Framework (permissions, isolation).

**Critères de validation** :
- Démarrage avec AVB activé (rejet d'image non signée).
- SELinux en mode enforcing (aucune violation non bloquée).
- Données utilisateur chiffrées au repos.
- Mise à jour OTA signée acceptée, mise à jour non signée rejetée.
- Protection anti-rollback fonctionnelle.
- Clés de signature stockées de manière sécurisée.

**Statut** : Non démarré.

## 3. Dépendances inter-modules (matrice)

| Module | Dépend de | Fournit à |
|--------|-----------|-----------|
| M-BL-001 | Matériel, clés AVB | M-KRN-001 |
| M-KRN-001 | M-BL-001, pilotes | M-HAL-001, M-DRV-*, M-SEC-001 |
| M-DRV-* | M-KRN-001, matériel | M-HAL-001 |
| M-HAL-001 | M-KRN-001, M-DRV-* | M-FWK-001, M-SYS-001 |
| M-FWK-001 | M-HAL-001, M-SYS-001 | M-UI-001, M-APP-001 |
| M-SYS-001 | M-HAL-001, M-KRN-001 | M-FWK-001, M-UI-001, M-SEC-001 |
| M-UI-001 | M-FWK-001, M-HAL-001, M-SYS-001 | M-APP-001 |
| M-APP-001 | M-FWK-001, M-UI-001, M-SYS-001 | — |
| M-SEC-001 | M-BL-001, M-KRN-001, M-SYS-001, M-FWK-001 | Tous (transversal) |

## 4. Critères de validation globaux

| Critère | ID lié | Moyen de vérification | Statut |
|---------|--------|----------------------|--------|
| Chaque module a une responsabilité définie | Tous | Ce document | v0.1 |
| Chaque module a des interfaces documentées | Tous | Ce document | v0.1 |
| Chaque module a des dépendances documentées | Tous | Matrice ci-dessus | v0.1 |
| Chaque module a des critères de validation | Tous | Ce document | v0.1 |
| Aucun test n'est déclaré réussi sans exécution | Tous | — | Respecté |

*Aucun des critères de validation ci-dessus n'a été exécuté à ce stade (dépôt vide, aucun matériel testé).*
| M-DRV-009 | Capteurs | Non démarré |