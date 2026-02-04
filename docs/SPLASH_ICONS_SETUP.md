# Configuration des Splash Screens et Icônes - Darassa Academy

## 🎯 Objectif
Remplacer les splash screens et icônes par défaut de Moodle par le branding personnalisé de Darassa Academy.

## ✅ Configuration effectuée

### 1. Fichiers de configuration modifiés
- **`config.xml`** : Configuration complète des splash screens et icônes
  - Couleur de fond principale : `#2E7D32` (vert Darassa)
  - Splash screen animé Android 12+ configuré
  - Toutes les densités d'écran supportées

### 2. Structure créée
```
resources/
├── android/
    ├── splash/
    │   ├── darassa_splash.xml          # Splash animé Android 12+
    │   └── README.md                   # Instructions détaillées
    └── icon/
        └── README.md                   # Instructions détaillées
```

### 3. Script d'automatisation
- **`scripts/setup-splash-icons.sh`** : Vérification automatique de la configuration

## 📱 Images à ajouter

### Splash Screens (12 images requises)
**Paysage :**
- `drawable-land-ldpi-screen.png` - 320x200px
- `drawable-land-mdpi-screen.png` - 480x320px  
- `drawable-land-hdpi-screen.png` - 800x480px
- `drawable-land-xhdpi-screen.png` - 1280x720px
- `drawable-land-xxhdpi-screen.png` - 1600x960px
- `drawable-land-xxxhdpi-screen.png` - 1920x1280px

**Portrait :**
- `drawable-port-ldpi-screen.png` - 200x320px
- `drawable-port-mdpi-screen.png` - 320x480px
- `drawable-port-hdpi-screen.png` - 480x800px
- `drawable-port-xhdpi-screen.png` - 720x1280px
- `drawable-port-xxhdpi-screen.png` - 960x1600px
- `drawable-port-xxxhdpi-screen.png` - 1280x1920px

### Icônes (10 images requises)
**Icônes principales :**
- `drawable-ldpi-icon.png` - 36x36px
- `drawable-mdpi-icon.png` - 48x48px
- `drawable-hdpi-icon.png` - 72x72px
- `drawable-xhdpi-icon.png` - 96x96px
- `drawable-xxhdpi-icon.png` - 144x144px
- `drawable-xxxhdpi-icon.png` - 192x192px

**Small Icons :**
- `drawable-ldpi-smallicon.png` - 18x18px
- `drawable-mdpi-smallicon.png` - 24x24px
- `drawable-hdpi-smallicon.png` - 36x36px
- `drawable-xhdpi-smallicon.png` - 48x48px

## 🎨 Design Guidelines

### Couleurs Darassa Academy
- **Vert principal** : `#2E7D32`
- **Vert clair** : `#4CAF50`
- **Blanc** : `#FFFFFF`

### Recommandations de design
- **Logo** : Symbole éducatif moderne (livre, mortier, etc.)
- **Texte** : "DA" ou "Darassa" si lisible
- **Style** : Épuré, professionnel, éducation
- **Fond** : Vert Darassa avec logo blanc

## 🚀 Application des changements

### 1. Ajouter les images
Placez toutes les images dans les dossiers appropriés :
```bash
# Splash screens
resources/android/splash/[fichiers].png

# Icônes  
resources/android/icon/[fichiers].png
```

### 2. Vérifier la configuration
```bash
# Exécuter le script de vérification
bash scripts/setup-splash-icons.sh
```

### 3. Rebuild l'application
```bash
# Nettoyer et reconstruire
ionic cordova clean android
ionic cordova build android
```

### 4. Tester
```bash
# Tester sur appareil
npm run dev:android
```

## ✅ Vérification

### Points à vérifier après build
- [ ] Splash screen s'affiche au lancement
- [ ] Logo Darassa Academy visible et centré
- [ ] Couleurs conformes au branding
- [ ] Affichage correct sur différentes tailles d'écran
- [ ] Icône de l'application correcte
- [ ] Small icon visible dans les notifications

## 🛠️ Dépannage

### Problèmes courants
1. **Splash screen Moodle s'affiche toujours**
   - Vérifier que `config.xml` contient bien la configuration Darassa
   - Nettoyer le projet : `ionic cordova clean android`

2. **Images non trouvées**
   - Vérifier les noms de fichiers exacts
   - Confirmer les dimensions requises

3. **Icône par défaut Android**
   - Ajouter les icônes dans tous les dossiers de densité
   - Rebuild après ajout des images

## 📋 Checklist finale

- [ ] 12 splash screens ajoutés
- [ ] 10 icônes ajoutées  
- [ ] `config.xml` configuré
- [ ] Build effectué sans erreurs
- [ ] Test sur appareil réussi
- [ ] Branding conforme à Darassa Academy

---

**Statut** : ✅ Configuration prête, images à ajouter  
**Prochaine action** : Ajouter les images de splash screen et icônes personnalisées
