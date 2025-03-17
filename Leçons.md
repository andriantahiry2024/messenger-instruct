# Leçons Apprises

## Architecture et Organisation du Code

### 1. Éviter la duplication des middlewares d'authentification

**Problème identifié**: Duplication de la logique d'authentification dans deux endroits différents:
- `messenger-clone/server/middleware/authMiddleware.js` - Un fichier dédié aux middlewares d'authentification
- `messenger-clone/server/controllers/authController.js` - Qui contient également une fonction `protect` similaire

**Solution**: 
- Centraliser tous les middlewares dans le dossier `middleware/`
- Utiliser uniquement le middleware défini dans `middleware/authMiddleware.js`
- Mettre à jour tous les imports dans les fichiers de routes pour pointer vers ce fichier

**Bonne pratique**:
- Suivre le principe DRY (Don't Repeat Yourself)
- Séparer clairement les responsabilités: les contrôleurs gèrent la logique métier, les middlewares gèrent les aspects transversaux comme l'authentification
- Maintenir une structure de projet cohérente pour faciliter la maintenance

### 2. Structure du projet Express.js

**Organisation recommandée**:
- `controllers/`: Logique métier et traitement des requêtes
- `middleware/`: Fonctions intermédiaires pour le traitement des requêtes
- `models/`: Définition des modèles de données
- `routes/`: Définition des routes API
- `config/`: Configuration de l'application
- `utils/`: Fonctions utilitaires

**Avantage**:
- Code plus maintenable et évolutif
- Séparation claire des responsabilités
- Facilite la collaboration entre développeurs

### 3. Cohérence des noms de fonctions entre routes et contrôleurs

**Problème identifié**: Incohérence entre les noms de fonctions exportées dans les contrôleurs et les noms utilisés dans les fichiers de routes:
- Dans `authController.js`: `registerUser`, `loginUser`, `getUserProfile`, `updateUserProfile`
- Dans `routes/auth.js`: `register`, `login`, `getProfile`, `updateProfile`

**Solution**:
- Assurer la cohérence des noms de fonctions entre les contrôleurs et les routes
- Standardiser les conventions de nommage dans toute l'application
- Vérifier les imports et les références de fonctions avant d'exécuter le serveur

**Bonne pratique**:
- Adopter une convention de nommage cohérente pour toute l'application
- Utiliser des noms descriptifs qui reflètent clairement la fonction
- Vérifier les références de fonctions après des modifications de noms

### 4. Gestion des dépendances

**Problème identifié**: Utilisation de modules non installés dans le code (`cookie-parser`, `express-async-handler`)

**Solution**:
- Vérifier que toutes les dépendances utilisées dans le code sont installées
- Installer les dépendances manquantes avec npm: `npm install cookie-parser express-async-handler`
- S'assurer que toutes les dépendances sont listées dans le fichier `package.json`

**Bonne pratique**:
- Maintenir à jour le fichier `package.json` avec toutes les dépendances
- Utiliser `npm install --save` pour ajouter automatiquement les dépendances au package.json
- Documenter les dépendances principales et leur utilité dans le README

### 5. Éviter les dossiers redondants

**Problème identifié**: Présence de deux dossiers avec des fonctionnalités similaires:
- `messenger-clone/server/middleware/` (singulier)
- `messenger-clone/server/middlewares/` (pluriel)

**Solution**:
- Standardiser les noms de dossiers (choisir soit singulier, soit pluriel)
- Supprimer les dossiers redondants
- Mettre à jour les imports pour pointer vers le bon dossier

**Bonne pratique**:
- Adopter une convention de nommage cohérente pour les dossiers
- Éviter la duplication de code et de structure
- Vérifier régulièrement la structure du projet pour éliminer les redondances

## Déploiement et Exécution

### 1. Exécution du serveur Node.js

**Problème identifié**: Erreur lors de l'exécution de `node server.js` depuis le mauvais répertoire

**Solution**:
- Toujours se positionner dans le répertoire du projet avant d'exécuter les commandes
- Utiliser `cd messenger-clone/server; node server.js` pour exécuter le serveur

**Bonne pratique**:
- Vérifier le répertoire courant avant d'exécuter des commandes
- Utiliser des scripts npm dans package.json pour standardiser les commandes d'exécution

### 2. Gestion des erreurs dans PowerShell

**Problème identifié**: L'opérateur `&&` n'est pas reconnu dans PowerShell comme séparateur de commandes

**Solution**:
- Utiliser l'opérateur `;` au lieu de `&&` dans PowerShell
- Exemple: `cd messenger-clone/server; node server.js`
- Alternativement, utiliser des scripts npm pour éviter les problèmes de syntaxe spécifiques au shell

**Bonne pratique**:
- Adapter les commandes au shell utilisé (PowerShell vs Bash)
- Utiliser des scripts npm pour assurer la portabilité entre différents environnements

### 3. Gestion des ports

**Problème identifié**: Erreur `EADDRINUSE: address already in use` lors du démarrage du serveur

**Solution**:
- Vérifier les processus utilisant le port avec `netstat -ano | findstr :PORT`
- Changer le port dans le fichier `.env` (de 5001 à 5002)
- Alternativement, arrêter le processus utilisant le port avec `taskkill /PID PROCESS_ID /F`

**Bonne pratique**:
- Configurer les ports dans les variables d'environnement pour faciliter les changements
- Implémenter une logique pour essayer des ports alternatifs si le port principal est occupé
- Documenter les ports utilisés par l'application dans le README 