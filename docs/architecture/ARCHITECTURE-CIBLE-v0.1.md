# Architecture cible — Zêblè OS v0.1

## Objet

Décrire les différentes couches de l'architecture cible, leurs relations et leurs dépendances.

## Statut

Proposition — en attente d'approbation par le fondateur.

## 1. Vue d'ensemble des couches

```
┌─────────────────────────────────────────────────────────┐
│                    Applications                         │
│  (Apps natives Zêblè, apps Android compatibles)         │
├─────────────────────────────────────────────────────────┤
│                    Interface utilisateur                │
│  (IHM inspirée bété / tapa / poids akan, langue FR)     │
├─────────────────────────────────────────────────────────┤
│                    Services système                     │
│  (Gestionnaire de paquets, OTA, énergie, compte, etc.)  │
├─────────────────────────────────────────────────────────┤
│                    Framework                            │
│  (API applicatives, gestion des ressources, intents)    │
├─────────────────────────────────────────────────────────┤
│                    HAL (Hardware Abstraction Layer)     │
│  (Abstraction des pilotes matériels)                    │
├─────────────────────────────────────────────────────────┤
│                    Pilotes                              │
│  (Périphériques : écran, tactile, caméra, modem, etc.)  │
├─────────────────────────────────────────────────────────┤
│                    Noyau Linux                          │
│  (Gestion mémoire, processus, pilotes, sécurité)        │
├─────────────────────────────────────────────────────────┤
│                    Bootloader                           │
│  (Initialisation, vérification AVB, chargement du noyau)│
└─────────────────────────────────────────────────────────┘
```

## 2. Description détaillée des couches

### 2.1 Bootloader

**Responsabilités** :
- Initialisation matérielle de base.
- Vérification de l'intégrité du noyau (Android Verified Boot - AVB).
- Chargement du noyau en mémoire.
- Passage de la main au noyau.

**Dépendances** :
- Matériel de référence (support du bootloader).
- Clés de signature AVB.
- Partition de démarrage du stockage.

**Sécurité** : AVB activé, aucune désautorisation pour les tests.

### 2.2 Noyau Linux

**Responsabilités** :
- Gestion de la mémoire et des processus.
- Gestion des pilotes périphériques.
- Gestion de l'énergie.
- SELinux en mode enforcing.
- Chiffrement du stockage (fscrypt ou équivalent).
- Protection anti-rollback.

**Dépendances** :
- Architecture matérielle (ARM64 à confirmer).
- Pilotes spécifiques au matériel de référence.
- Configuration du bootloader.

**Sécurité** : SELinux enforcing, chiffrement activé, aucune protection désactivée.

### 2.3 Pilotes

**Responsabilités** :
- Contrôle direct du matériel : écran tactile, écran d'affichage, GPU, caméra, modem, Wi-Fi, Bluetooth, audio, capteurs, boutons.

**Dépendances** :
- Noyau Linux (interface de pilotes).
- HAL (abstraction vers le framework).
- Spécifications matérielles de l'appareil de référence.

**Exemples de pilotes requis** :
- Écran et tactile (framebuffer, toucher).
- GPU (accélération graphique).
- Caméra (capture photo/vidéo).
- Modem (4G/5G, appels, SMS).
- Wi-Fi et Bluetooth.
- Audio (haut-parleur, microphone, prise jack/USB-C).
- Gestion énergétique (batterie, charge).

### 2.4 HAL (Hardware Abstraction Layer)

**Responsabilités** :
- Abstraction des pilotes matériels pour le framework.
- Interfaces standardisées entre le matériel et les services système.
- Mise à disposition des fonctionnalités matérielles via des API stables.

**Dépendances** :
- Pilotes.
- Noyau Linux.

### 2.5 Framework

**Responsabilités** :
- API applicatives pour le développement d'applications.
- Gestion du cycle de vie des applications.
- Gestion des ressources (fenêtres, affichage, saisie).
- Gestion des permissions.
- Intents et communication inter-applications.

**Dépendances** :
- HAL.
- Services système.
- Noyau Linux (via les pilotes et la HAL).

**Compatibilité Android** : si le framework est basé sur AOSP, compatibilité partielle avec les applications Android à vérifier par tests réels.

### 2.6 Services système

**Responsabilités** :
- Gestionnaire de paquets (installation, mise à jour, suppression d'applications).
- Gestionnaire d'OTA (téléchargement, vérification de signature, installation des mises à jour).
- Gestion de l'énergie (veille, réveil, optimisation de la batterie).
- Gestion des comptes et de l'authentification.
- Gestion des notifications.
- Gestion du stockage et du chiffrement.

**Dépendances** :
- Framework.
- HAL.
- Noyau Linux (chiffrement, gestion de l'énergie).

### 2.7 Interface utilisateur

**Responsabilités** :
- Affichage de l'interface graphique.
- Gestion du tactile.
- Thème visuel original inspiré des signes bété, du tapa et de la géométrie des poids akan.
- Langue initiale : français.
- Accessibilité pour smartphones économiques.

**Dépendances** :
- Framework.
- HAL (écran, tactile).
- Services système (notifications, comptes).

### 2.8 Applications

**Responsabilités** :
- Applications natives Zêblè OS.
- Applications Android (si compatibilité démontrée).

**Dépendances** :
- Framework.
- Interface utilisateur.
- Services système.

### 2.9 Mécanismes de sécurité et de mise à jour

**Responsabilités** :
- Android Verified Boot (AVB) : chaîne de confiance du bootloader au système.
- SELinux en mode enforcing : confinement des processus.
- Chiffrement des données utilisateur.
- Mises à jour OTA signées.
- Protection anti-rollback.
- Gestion des clés de chiffrement et de signature.
- Isolation des applications (sandbox).
- Modèle de permissions.

**Dépendances** :
- Bootloader (AVB).
- Noyau Linux (SELinux, chiffrement).
- Services système (OTA).
- Framework (permissions, isolation).

## 3. Relations et dépendances entre les couches

```
Applications → Interface utilisateur → Services système → Framework → HAL → Pilotes → Noyau → Bootloader
     ↑                                                                    ↓
     └──────────────────── Sécurité et mise à jour (transversal) ─────────┘
```

**Règle de dépendance** : Une couche supérieure ne dépend que de la couche immédiatement inférieure (et des couches transversales de sécurité). Aucune dépendance circulaire n'est autorisée.

## 4. Hypothèses et zones d'incertitude

| Élément | Hypothèse | Statut |
|---------|-----------|--------|
| Architecture matérielle | ARM64 | À confirmer selon l'appareil de référence |
| Base système | AOSP en cours d'étude | Non décidé |
| Compatibilité Android | À vérifier par tests réels | Non démontré |
| Appareil de référence | Non sélectionné | À sélectionner |

*Aucune de ces hypothèses n'a été validée à ce stade (dépôt vide, aucun matériel testé).*
- Framework (consommateur des services HAL).