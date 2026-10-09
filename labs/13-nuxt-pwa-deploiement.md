# LAB 13 — Nuxt, PWA et déploiement

**Durée indicative :** 1 à 2 jours.  
**Prérequis :** Vue, routes, API et build de production.

## Partie A — Comprendre avant d'adopter Nuxt
Explique les différences entre rendu côté client (CSR), rendu côté serveur (SSR) et génération statique (SSG). Décris les compromis : référencement, temps de première réponse, coût serveur, données personnalisées et complexité opérationnelle.

Crée une petite application Nuxt seulement après avoir compris les pages, layouts, composants, composables et chargement de données. Compare sa structure à une application Vue + Vite.

## Partie B — Rendu et données
- Distingue les données publiques et personnalisées.
- Évite d'accéder directement à des API navigateur pendant le rendu serveur.
- Vérifie les erreurs, le chargement et les états vides.
- Vérifie que les données utilisées lors du rendu initial sont compatibles avec l'hydratation.
- Ne mets aucun secret dans le code exécuté côté client.

## Partie C — PWA
Définis ce qu'apporte une PWA et ce qu'elle ne garantit pas automatiquement.
- Prépare un manifeste avec nom, icônes et mode d'affichage.
- Comprends le rôle du service worker.
- Décide explicitement quelles ressources peuvent être mises en cache.
- Prévois comment informer l'utilisateur d'une mise à jour.
- Teste l'application en mode réseau dégradé.

Ne mets pas en cache aveuglément les réponses contenant des données privées. Une mauvaise stratégie de cache peut exposer ou afficher des données périmées.

## Partie D — Build et déploiement
1. Vérifie le script de build.
2. Lance le build local.
3. Configure les variables d'environnement adaptées à l'hébergement.
4. Vérifie que les valeurs publiques ne contiennent pas de secrets.
5. Déploie une version de test.
6. Vérifie les routes directes, le rafraîchissement d'une page et les ressources.
7. Observe les erreurs console et serveur.
8. Documente le retour à la version précédente si la plateforme le permet.

## Critères d'acceptation
- [ ] Je peux expliquer CSR, SSR, SSG et hydratation.
- [ ] Je sais pourquoi certaines API navigateur ne sont pas disponibles côté serveur.
- [ ] Je peux expliquer les règles de cache du service worker.
- [ ] Le build de production réussit.
- [ ] Les routes directes fonctionnent après déploiement.
- [ ] Aucune valeur secrète n'est livrée au navigateur.
- [ ] Le README permet à une autre personne de lancer le projet.

## Questions
1. Pourquoi ne pas choisir SSR pour chaque application ?
2. Pourquoi une PWA peut-elle afficher des données périmées ?
3. Quelle différence entre variable privée du serveur et variable publique frontend ?
4. Quelles vérifications faire après un déploiement ?