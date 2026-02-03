# Configuration de l'environnement de développement Android

## Vue d'ensemble
Ce document décrit la configuration de l'environnement de développement Android pour l'application mobile Darassa Academy basée sur Moodle.

## Prérequis

### Système
- **Node.js** : version >=v22.17 <25
- **npm** : dernière version
- **Android Studio** : dernière version stable
- **Java Development Kit** : JDK 17 ou plus récent

### Configuration Android
- **Android SDK** : API 24 minimum (Android 7.0)
- **Target SDK** : API 36 (Android 14)
- **Gradle** : 8.13

## Installation et configuration

### 1. Installation des dépendances
```bash
npm install
```

### 2. Installation d'Ionic CLI
```bash
npm install -g @ionic/cli
```

### 3. Configuration de la plateforme Android
```bash
ionic cordova platform add android
```

### 4. Construction du projet Android
```bash
ionic cordova build android
```

## Lancement de l'application

### Développement avec live reload
```bash
npm run dev:android
```

### Build de production
```bash
npm run prod:android
```

### Ouverture dans Android Studio
```bash
ionic cordova open android
```

## Structure du projet Android

### Fichiers de configuration clés
- `config.xml` : Configuration Cordova globale
- `platforms/android/` : Projet Android généré
- `resources/android/` : Ressources Android (icônes, splash screens)
- `google-services.json` : Configuration Firebase pour Android

### Configuration de l'application
- **Nom de l'application** : Darassa Academy
- **Package ID** : com.darassa.academy
- **Version** : 5.1.0 (51001)

## Résultat du build

Le build génère un APK de débogage à l'emplacement :
```
platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

## Dépannage

### Problèmes courants

1. **Ionic non reconnu**
   ```bash
   npm install -g @ionic/cli
   ```

2. **Problèmes de permissions Android**
   - Vérifier la configuration dans `config.xml`
   - S'assurer que les permissions nécessaires sont déclarées

3. **Erreurs de build Gradle**
   - Nettoyer le projet : `ionic cordova clean android`
   - Rebuild : `ionic cordova build android`

### Logs et rapports
- Rapports de build : `platforms/android/build/reports/`
- Logs de l'application : Utiliser Android Studio Logcat

## Déploiement

### Pour le développement
1. Connecter un appareil Android via USB
2. Activer le débogage USB
3. Lancer : `npm run dev:android`

### Pour la production
1. Générer le build de production : `npm run prod:android`
2. Signer l'APK avec la clé de production
3. Uploader sur Google Play Console

## Notes importantes

- Le projet utilise Cordova pour le développement multiplateforme
- L'application est configurée pour utiliser Firebase (Google Services)
- Les ressources graphiques sont optimisées pour différentes densités d'écran
- Le support AndroidX est activé pour la compatibilité avec les dernières versions d'Android

## Mise à jour

Pour mettre à jour les dépendances Android :
```bash
ionic cordova platform update android
```

Pour mettre à jour les plugins :
```bash
ionic cordova plugin update
```

---

**Date de création** : 3 février 2026
**Version** : 1.0
**Auteur** : Équipe de développement Darassa Academy
