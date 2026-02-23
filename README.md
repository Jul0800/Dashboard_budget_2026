# Déploiement sur Netlify — Budget Dashboard 2026

Ce guide explique comment déployer le Budget Dashboard 2026 sur Netlify.

## Prérequis

- Un compte GitHub avec le repository du projet
- Un compte Netlify (gratuit sur [netlify.com](https://netlify.com))
- Node.js 22+ et pnpm installés localement

## Méthode 1 : Déploiement via Netlify UI (Recommandé)

### Étape 1 : Préparer le repository GitHub

1. Assurez-vous que le projet est poussé sur GitHub
2. Le repository doit contenir les fichiers `netlify.toml` et `.netlifyignore` (déjà inclus)

### Étape 2 : Connecter Netlify à GitHub

1. Allez sur [app.netlify.com](https://app.netlify.com)
2. Cliquez sur **"Add new site"** → **"Import an existing project"**
3. Sélectionnez **GitHub** comme provider
4. Autorisez Netlify à accéder à vos repositories
5. Sélectionnez le repository `budget-dashboard-2026`

### Étape 3 : Configurer les paramètres de build

Netlify lira automatiquement `netlify.toml`. Vérifiez que :

- **Build command** : `pnpm install && pnpm run build`
- **Publish directory** : `dist/public`
- **Node version** : 22.13.0 (défini dans netlify.toml)

### Étape 4 : Déployer

Cliquez sur **"Deploy site"**. Netlify va :
1. Cloner le repository
2. Installer les dépendances (`pnpm install`)
3. Construire le projet (`pnpm run build`)
4. Déployer le contenu de `dist/public`

Le site sera accessible à une URL comme `https://budget-dashboard-2026.netlify.app`

## Méthode 2 : Déploiement via CLI Netlify

### Étape 1 : Installer Netlify CLI

```bash
npm install -g netlify-cli
```

### Étape 2 : Construire le projet localement

```bash
cd budget-dashboard-2026
pnpm install
pnpm run build
```

### Étape 3 : Déployer

```bash
netlify deploy --prod --dir=dist/public
```

Netlify vous demandera de vous connecter et de créer un nouveau site.

## Domaine personnalisé

### Ajouter un domaine personnalisé

1. Dans Netlify, allez sur **Site settings** → **Domain management**
2. Cliquez sur **Add custom domain**
3. Entrez votre domaine (ex: `budget.example.com`)
4. Suivez les instructions pour mettre à jour les DNS

### Configuration DNS

Netlify vous fournira les enregistrements DNS à ajouter chez votre registrar :
- Enregistrements A ou ALIAS pointant vers Netlify
- Certificat SSL/TLS automatique via Let's Encrypt

## Variables d'environnement

Si vous avez besoin de variables d'environnement :

1. Allez sur **Site settings** → **Build & deploy** → **Environment**
2. Cliquez sur **Edit variables**
3. Ajoutez vos variables (ex: `VITE_API_URL`)

Les variables seront injectées pendant le build.

## Déploiements automatiques

Netlify déploiera automatiquement à chaque push sur la branche principale (main/master).

Pour configurer d'autres branches :
1. **Site settings** → **Build & deploy** → **Deploy contexts**
2. Configurez les branches pour preview et production

## Monitoring et logs

### Voir les logs de build

1. Allez sur **Deploys**
2. Cliquez sur un déploiement
3. Consultez **Deploy log** pour les détails

### Analytics

Netlify propose des analytics gratuites :
- **Analytics** → Activez les analytics du site
- Suivi des visites, performances, etc.

## Optimisations

### Caching

Le fichier `netlify.toml` inclut des en-têtes de cache :
- Assets versionnés (avec hash) : cache 1 an
- Autres fichiers : cache court (validation requise)

### Compression

Netlify compresse automatiquement les assets (gzip, brotli).

### Optimisation des images

Pour optimiser les images, utilisez Netlify Image CDN :
```html
<img src="/.netlify/images?url=https://example.com/image.jpg&w=400" />
```

## Troubleshooting

### Build échoue avec erreur "pnpm not found"

Assurez-vous que `node_version` est >= 16 dans `netlify.toml`. pnpm est inclus par défaut.

### Site affiche 404 pour les routes

Vérifiez que le redirect `/* → /index.html` est dans `netlify.toml`. C'est nécessaire pour le client-side routing.

### Données localStorage perdues après déploiement

C'est normal — localStorage est spécifique au navigateur/domaine. Les données persistent sur le même domaine.

### Certificat SSL ne fonctionne pas

Attendez 24-48h après l'ajout du domaine. Netlify génère le certificat automatiquement.

## Support

- Documentation Netlify : https://docs.netlify.com
- Support Netlify : https://support.netlify.com
- GitHub Issues : Signalez les bugs du projet

---

**Budget Dashboard 2026** est maintenant prêt pour Netlify ! 🚀
