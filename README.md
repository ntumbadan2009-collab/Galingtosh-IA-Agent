# Galingtosh Web

Version web fidèle à l'application Android Galingtosh (Expo / React Native / TypeScript). Le client web reprend les écrans et les contrats fonctionnels de l'APK, avec les adaptations nécessaires aux navigateurs.

## Fonctionnalités reproduites

- Studio conversationnel relié à Supabase Edge Function `chat-agent`.
- Création, liste et reprise des projets via les tables `projects`, `conversations` et `messages`.
- Authentification e-mail/mot de passe, inscription, récupération de compte et OAuth Google.
- Import d'images, vidéos et fichiers audio dans le bucket privé `user-uploads` (50 Mo maximum, 10 pièces jointes par message).
- Médiathèque, licences et médias associés aux projets.
- Consultation du Film JSON versionné, de ses scènes et de ses plans.
- Demande de rendu via `request-render`, suivi de progression, erreurs, avertissements et annulation.
- Ouverture de la vidéo MP4 via URL signée du bucket `renders`.
- PWA installable avec cache de l'interface uniquement. Les API, sessions privées, données, médias et rendus ne sont pas mis en cache hors ligne.

## Architecture et sécurité

- Même projet Supabase : Auth, PostgreSQL, Storage et Edge Functions.
- Même moteur Render : `https://galingtosh-engine.onrender.com`, via les fonctions Supabase existantes.
- Seule la clé publique Supabase publishable/anon est embarquée dans le client. Aucune clé `service_role` ni aucun secret du moteur n'est inclus.
- Le dépôt Android n'est ni modifié ni utilisé comme cible de déploiement.

## Développement

Node.js 22 recommandé.

```bash
npm install
npm run typecheck
npm run start
npm run build:web
```

## GitHub Pages

Le workflow `.github/workflows/deploy-pages.yml` construit l'application, vérifie TypeScript et publie `dist/` sur GitHub Pages à chaque push sur `main`.

1. Dans **Settings → Pages**, choisir **GitHub Actions** comme source de déploiement.
2. Le dépôt est actuellement privé. Avec GitHub Free, GitHub Pages pour un dépôt privé nécessite de rendre le dépôt public ou d'utiliser un plan GitHub qui autorise les Pages privés. La visibilité n'est pas modifiée automatiquement.
3. Après activation, ajouter l'URL exacte de l'application (par défaut `https://ntumbadan2009-collab.github.io/Galingtosh-IA-Agent/`) aux URL de redirection autorisées dans Supabase Auth et vérifier le fournisseur Google.

Aucun domaine personnalisé n'est configuré à cette étape.

## Hors connexion

La PWA met en cache les ressources statiques de l'interface pour ouvrir la coque de l'application hors connexion. Les conversations, projets, médias, authentification et rendus nécessitent Internet.
