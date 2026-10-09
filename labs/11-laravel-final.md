# LAB 11 — Intégrer Vue 3 à une API Laravel

**Durée indicative :** 2 à 4 jours.  
**Prérequis :** CRUD, fetch, routes, état partagé et gestion d'erreurs.

## Partie 1 — Contrat avant le code
Pour chaque endpoint, note méthode et URL, paramètres, authentification, exemple de requête, réponse de succès, erreurs possibles, pagination et autorisations. Vérifie les routes réelles au lieu de deviner.

## Partie 2 — Configuration
- Place l'URL de base dans une variable d'environnement frontend appropriée.
- Les variables VITE_* sont intégrées au code visible dans le navigateur : ce ne sont pas des secrets.
- Prévois une configuration développement et une configuration production.
- Vérifie CORS et le mécanisme d'authentification du backend sans désactiver les protections.

## Partie 3 — Flux CRUD
Implémente progressivement la liste, le détail, la création, la modification et la suppression avec confirmation. Pour chaque action, gère chargement, succès, échec et actualisation cohérente.

## Partie 4 — Erreurs Laravel
- Affiche les erreurs de validation sous les champs correspondants.
- Distingue validation (souvent 422), authentification, autorisation, ressource introuvable, erreur serveur et problème réseau.
- Ne montre jamais de stack trace à l'utilisateur.
- Le backend valide toutes les données, même si le frontend a déjà validé.

## Partie 5 — Authentification
Choisis un flux compatible avec le backend réel, par exemple une session/cookies si le projet utilise ce modèle. Respecte CSRF et la configuration du framework. Une route masquée côté frontend n'empêche pas l'appel direct à l'API : le backend doit vérifier les permissions pour chaque action sensible.

## Partie 6 — Vérifications
- [ ] URL de base configurée sans secret exposé.
- [ ] Contrat correspondant aux routes réelles.
- [ ] États loading/error/empty/success.
- [ ] Erreurs 422 liées aux champs.
- [ ] Erreurs 401/403/404/500 gérées.
- [ ] Doubles soumissions évitées lorsque nécessaire.
- [ ] Actions interdites refusées par le backend.
- [ ] Tests des règles métier critiques.
- [ ] Build de production réussi.
- [ ] README d'installation et de configuration.

## Livraison
Fournis un dépôt propre, documentation, schéma d'architecture, contrat API, captures, tests et présentation orale de 5 à 10 minutes.

## Questions d'entretien
1. Pourquoi Vue ne décide-t-il pas seul des permissions ?
2. Pourquoi 422 n'est-il pas la même chose qu'une erreur réseau ?
3. Pourquoi une variable VITE_* n'est-elle pas secrète ?
4. Comment diagnostiquer CORS ?
5. Quelle différence entre l'état Pinia et la donnée confirmée par Laravel ?