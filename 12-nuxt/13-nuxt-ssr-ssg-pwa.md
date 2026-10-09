# Module 13 — Nuxt, SSR, SSG et PWA

## Nuxt
Nuxt est un framework construit autour de Vue qui apporte des conventions et des capacités serveur. Il convient à certains projets mais n'est pas obligatoire pour toute application Vue.

Étudie les pages, layouts, composants, composables, plugins, middleware et le chargement de données avec la documentation Nuxt actuelle.

## Rendu
- CSR : le navigateur construit l'interface à partir du JavaScript chargé.
- SSR : le serveur génère le HTML pour une requête.
- SSG : les pages sont générées à l'avance au build.
- Hydratation : Vue reprend côté client une interface HTML déjà rendue.

Chaque stratégie a des compromis en performance, déploiement, données dynamiques et complexité. Attention au code qui dépend de `window` ou `document` lors du rendu serveur.

## PWA
Une Progressive Web App peut proposer un manifeste, une installation et un service worker. Le cache doit être conçu prudemment : des données périmées ou privées ne doivent pas être mises en cache de façon inappropriée. Prévois une stratégie de mise à jour et un comportement hors ligne compréhensible.

## Laboratoire
Prends une application catalogue et documente :
1. pourquoi une SPA Vue simple suffit ou non ;
2. les avantages et limites d'un rendu serveur ;
3. les pages qui pourraient être statiques ;
4. les données qui ne doivent pas être mises en cache ;
5. le parcours d'installation et de mise à jour d'une PWA.

Ne commence l'implémentation avancée qu'après avoir maîtrisé Vue 3, Router, les API et les tests.
