# Plan de formation Vue.js

## Objectif général
Savoir concevoir, construire, tester, maintenir et déployer une application Vue 3, tout en comprenant les responsabilités des composants et des outils.

## Phase A — Socle web
1. Navigateur, client/serveur, HTTP, DOM et console.
2. HTML sémantique, formulaires et accessibilité de base.
3. CSS : cascade, box model, Flexbox, Grid, responsive.
4. JavaScript : variables, types, conditions, boucles, fonctions.
5. Tableaux, objets, méthodes, immutabilité et transformations.
6. Modules ES, imports/exports, destructuration et opérateurs modernes.
7. Portée, closures, callbacks, promesses, async/await et erreurs.
8. Git : status, diff, add, commit, branch, merge, conflits.

**Validation :** manipuler un tableau d'objets de produits en JavaScript sans Vue.

## Phase B — Vue 3 fondamental
9. Pourquoi Vue, SPA, Vue 3, Vite et structure du projet.
10. SFC : template, script setup et style.
11. Interpolation, expressions et attributs.
12. Directives : v-bind, v-on, v-if, v-show, v-for, v-model.
13. Événements, modificateurs et événements clavier.
14. Réactivité : ref, .value en JavaScript, déballage dans les templates.
15. reactive, limites de destructuration et cas d'usage.
16. computed : valeur dérivée, cache et différence avec une méthode.
17. watch et watchEffect : effets secondaires et nettoyage.
18. Classes/styles dynamiques, listes, clés stables et rendu conditionnel.
19. Gestion des erreurs, états vides et chargement.
20. Composants simples et séparation template/logique/styles.

**Validation :** catalogue de plats avec recherche, filtre, stock et total.

## Phase C — Composants et conception
21. Composition API et script setup.
22. Props avec defineProps : contrat parent-enfant et validation.
23. Événements avec defineEmits : remonter une intention, pas modifier la prop.
24. Slots nommés et slot par défaut.
25. Composants contrôlés, v-model sur un composant.
26. Composants dynamiques, KeepAlive et composants asynchrones.
27. Cycle de vie : onMounted, onUpdated, onUnmounted.
28. Template refs et accès au DOM avec parcimonie.
29. Composables : extraire et partager la logique.
30. Architecture : pages, composants, composables, services et types.

**Validation :** interface découpée en composants réutilisables avec responsabilités expliquées.

## Phase D — Données et navigation
31. Formulaires, validation, messages d'erreur et accessibilité.
32. CRUD local : créer, lire, modifier, supprimer.
33. localStorage, JSON, synchronisation et limites de la persistance navigateur.
34. HTTP, JSON, fetch, méthodes, statuts et en-têtes.
35. API : états loading/error/empty/success, annulation et course de requêtes.
36. Pagination, recherche, tri et filtres côté client ou serveur.
37. Vue Router : routes, RouterLink, RouterView et navigation.
38. Paramètres, query strings, routes imbriquées et layouts.
39. Guards, routes privées et gestion d'une session.
40. Pinia : state, getters, actions, stores et organisation.
41. Stratégie d'état : local vs URL vs serveur vs store global.

**Validation :** boutique multi-pages avec panier persistant et données API.

## Phase E — Qualité professionnelle
42. TypeScript : types, interfaces, unions, generics de base et props typées.
43. Tests unitaires : Vitest.
44. Tests de composants : Vue Test Utils, props, emits et interactions.
45. Tests de parcours : Playwright.
46. ESLint, formatage, conventions et revues de code.
47. Accessibilité : labels, clavier, focus, contraste et annonces.
48. Sécurité frontend : XSS, validation côté serveur, secrets et dépendances.
49. Performance : lazy loading, code splitting, rendu de listes et mesures.
50. Environnements, variables publiques, build et déploiement.

**Validation :** tests utiles, build reproductible et parcours critiques documentés.

## Phase F — Écosystème avancé
51. Nuxt : conventions, pages, layouts, plugins, composables et data fetching.
52. SSR, CSR, SSG, hydratation et compromis.
53. PWA : manifest, service worker, cache et mises à jour.
54. Upload de fichiers, prévisualisation et limites côté client.
55. Authentification : flux, cookies, CSRF, CORS et rôles.
56. Intégration avec Laravel : API, erreurs de validation, pagination et auth.
57. Déploiement, variables d'environnement, logs et diagnostic en production.
58. Maintenance : migrations de dépendances, dette technique et documentation.

## Calendrier intensif indicatif (30 jours)
- J1–4 : socle JavaScript et démarrage Vue.
- J5–9 : réactivité et composants.
- J10–13 : formulaires, CRUD et API.
- J14–17 : Router et Pinia.
- J18–21 : composables, TypeScript et architecture.
- J22–24 : tests, accessibilité, sécurité et performance.
- J25–28 : projet complet connecté à une API.
- J29 : corrections, tests et déploiement.
- J30 : évaluation finale.

Si les évaluations montrent une incompréhension, reprendre la notion avant de poursuivre. La vitesse ne remplace pas la maîtrise.
