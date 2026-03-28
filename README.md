# PROJET 1986 : RÉACTIVATION

Escape game immersif pour un anniversaire de 40 ans.  
PWA installable, jouable offline sur mobile.

## Structure des fichiers

```
projet1986-pwa/
├── index.html      ← Application principale (tout-en-un)
├── manifest.json   ← Manifeste PWA (install sur mobile)
├── sw.js           ← Service Worker (cache offline)
├── Fouras.m4a      ← Audio énigme Père Fouras
├── icons/
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

## Déploiement sur GitHub Pages

### 1. Créer le repo

```bash
git init
git add .
git commit -m "Projet 1986 v1"
git branch -M main
git remote add origin https://github.com/TON_USER/projet1986.git
git push -u origin main
```

### 2. Activer GitHub Pages

1. Va dans **Settings** → **Pages**
2. Source : **Deploy from a branch**
3. Branch : `main` / `/ (root)`
4. Clique **Save**
5. Attends 1-2 min → ton site est live sur `https://TON_USER.github.io/projet1986/`

### 3. Corriger le chemin si sous-dossier

Si l'URL est `https://user.github.io/projet1986/` (pas à la racine),
modifie `manifest.json` :

```json
"start_url": "/projet1986/",
```

Et dans `sw.js`, préfixe les chemins :

```js
const BASE = '/projet1986';
const ASSETS = [
  BASE + '/',
  BASE + '/index.html',
  BASE + '/Fouras.m4a',
  // etc.
];
```

### 4. Installer sur le téléphone

1. Ouvre l'URL dans **Chrome** (Android) ou **Safari** (iOS)
2. Android : le navigateur proposera "Ajouter à l'écran d'accueil" automatiquement
3. iOS : bouton partage → "Sur l'écran d'accueil"
4. L'app se lance en plein écran comme une vraie app

## Fonctionnalités

- 17 énigmes en 4 actes
- Sauvegarde locale (localStorage) — la progression persiste
- Audio intégré (Père Fouras)
- Interactions : lampe torche, clavier numérique, taquin, NFC simulé, GPS simulé
- Faux bug système
- Fonctionne hors ligne après premier chargement
- Barre DEV en bas pour tester (SKIP / SOLVE ALL / RESET)

## Pour la version de prod

- **Retirer la barre DEV** : supprimer le `<div class="dev-bar">` dans `index.html`
- **Ajouter Supabase** (optionnel) : pour sync de progression cross-device
- **Ajouter les vraies interactions NFC/GPS** avec les APIs Web
- **Wrapper en APK** (si besoin) : utiliser Codemagic + un projet Flutter WebView
