# Projet Calculette Vectorielle sur LPC55S69 - Travail Étudiant 1

## Tâches de l'Étudiant 1

Ce dépôt contient la partie du projet calculette vectorielle réalisée par l'étudiant 1, principalement axée sur :
1. La gestion des séquences VT100 (interface terminal)
2. La carte SD et système de fichiers FAT
3. Le raccordement de la libc à FatFS

## 🖥️ Interface Terminal avec Séquences VT100

### Objectifs
- Améliorer l'interface utilisateur du terminal série
- Implémenter les commandes d'édition (flèches, backspace)
- Ajouter la coloration de l'interface

### Implémentations réalisées
- Reconnaissance des séquences VT100 pour les touches de navigation et fonctions
- Synchronisation du curseur entre la fonction d'édition et le terminal
- Coloration des différents modes (édition, erreur, résultat)
- Historique des commandes accessible avec les flèches haut/bas

## 💾 Carte SD et Système de Fichiers FAT

### Objectifs
- Accéder à la carte SD via le protocole SDIO
- Implémenter le système de fichiers FAT pour stocker/charger des calculs
- Gestion des opérations de base sur les fichiers (ls, cd, mkdir, rm)

### Implémentations réalisées
- Configuration du contrôleur SDIO et initialisation de la carte SD
- Intégration de FatFS pour la gestion du système de fichiers
- Implémentation des fonctions de navigation dans l'arborescence
- Gestion des événements de connexion/déconnexion de la carte

### Structure de la mémoire
- Flash (640kB): 0x00000000 - 0x0009FFFF
- SRAMX (32kB), CPU1 code: 0x04000000 - 0x04007FFF
- CPU0 SRAM (96kB), data, stack and heap: 0x20000000 - 0x20017FFF
- calc SRAM stack (96kB): 0x20018000 - 0x2002FFFF

## 🔄 Raccordement de la libc à FatFS

### Objectifs
- Faire le lien entre les fonctions standard de la libc et FatFS
- Permettre l'utilisation des fonctions open, read, write, close

### Implémentations réalisées
- Adaptation des fonctions _open, _read, _write, _close
- Gestion des descripteurs de fichiers et conversion des flags
- Structure de données pour stocker les références aux fichiers ouverts

## 🔧 Configuration technique

- Microcontrôleur : NXP LPC55S69 (dual Cortex-M33)
- Interface série : 115200 bauds, pas de parité, 1 bit de stop
- IDE : MCUXpresso
- Dépendances : FatFS (http://elm-chan.org/fsw/ff/00index_e.html)

## ▶️ Comment tester

1. Connecter la carte LPC55S69 via USB
2. Ouvrir un terminal série (115200 bauds, 8N1)
3. Insérer une carte microSD formatée en FAT32
4. Essayer les commandes suivantes:
   - `ls` - Lister les fichiers
   - `cd dossier` - Changer de répertoire
   - `a=1:10` - Créer un vecteur
   - `dump test.txt` - Sauvegarder les commandes
   - `help` - Afficher l'aide (si help.txt est présent)

## 📝 Notes d'implémentation

- Les séquences VT100 permettent l'édition complète avec les flèches
- Le système reconnaît l'insertion/suppression de la carte SD en temps réel
- L'interfaçage libc/FatFS permet d'utiliser les fonctions standard C pour accéder à la carte SD

## 🔍 Limitations connues

- Les fonctions de libc sont limitées aux opérations basiques (pas de seek, etc.)
- Le nombre de fichiers ouverts simultanément est limité
- La détection de la carte SD peut parfois nécessiter un redémarrage du système

---

*Ce projet fait partie d'un travail pédagogique plus large sur le microcontrôleur LPC55S69 à l'ENIB*