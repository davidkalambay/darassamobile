# Langue française dans Darassa Mobile

Pour que l’application s’affiche en français par défaut, deux points sont gérés.

## 1. Priorité à la langue forcée (déjà en place)

Dans `moodle.config.json` vous avez :

- `"default_lang": "fr"`
- `"forcedefaultlanguage": true`

Le code a été ajusté pour que, lorsque `forcedefaultlanguage` est activé, la langue utilisée soit toujours `default_lang` (français), et non la langue du téléphone ni une ancienne préférence stockée.

## 2. Fichier de traductions françaises (fr.json)

Les textes de l’app sont chargés depuis `src/assets/lang/*.json`. Seul `en.json` est souvent présent par défaut. Pour le français, il faut générer `fr.json` à partir des packs de langue Moodle Mobile.

**À faire avant de builder l’app :**

1. Installer **jq** (et avoir **git**).
2. Depuis la racine du projet, aller dans le dossier des scripts et lancer le script de mise à jour des langues :

```bash
cd scripts
./update_langpacks.sh
```

Le script :

- récupère les packs de langue Moodle Mobile (version lue dans `moodle.config.json`, ex. 5.1),
- copie les langues listées dans `moodle.config.json` (dont `fr`) vers `src/assets/lang/`,
- crée notamment `src/assets/lang/fr.json`.

3. Rebuilder l’app (ex. `npm run build` ou votre commande Cordova/Ionic habituelle).

**Sous Windows :** exécuter le script dans **Git Bash** ou **WSL** (bash requis).

Après un build avec `fr.json` présent et `forcedefaultlanguage: true`, l’application doit s’ouvrir en français.
