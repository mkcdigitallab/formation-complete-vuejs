# Formation complète Vue.js — du débutant au développeur autonome

> Objectif : maîtriser Vue 3 et son écosystème en comprenant les principes, en construisant des projets, en déboguant et en justifiant ses choix. Ce dépôt est un vrai parcours de formation : le cours explique les notions avant de demander de les appliquer.

## Commencer ici — le cours complet

**Lis d'abord le [Cours complet Vue 3](COURS-COMPLET-VUE3.md).** Il reprend les fondations du web, JavaScript, Vue, les templates, la réactivité, les composants, les formulaires, les API, le routage, Pinia, TypeScript, les tests, la qualité, Nuxt, les PWA et l'intégration Laravel. Les notions sont expliquées avant les exercices, avec leur utilité, leurs limites et les erreurs fréquentes.

Ensuite, suis cet ordre :

1. [Plan détaillé de formation](PLAN-DE-FORMATION.md) — parcours complet et validations.
2. [Guide de l'apprenant](GUIDE-APPRENANT.md) — méthode pour étudier et pratiquer.
3. [LAB 00 : préparer l'environnement](labs/00-preparer-environnement.md).
4. Suis les modules dans l'ordre ci-dessous.
5. Coche le [suivi de progression](SUIVI-DE-PROGRESSION.md) seulement quand tu peux expliquer et réutiliser la notion.
6. Applique la [méthode de résolution de problèmes](METHODE-DE-RESOLUTION.md) quand un comportement est inattendu.
7. Termine les projets et la [grille d'évaluation de maîtrise](evaluations/grille-maitrise.md).

## Parcours de cours

| Étape | Contenu |
|---|---|
| 01 | [Découvrir Vue](01-fondamentaux/01-decouvrir-vue.md) |
| 02 | [Templates et directives](01-fondamentaux/02-templates-directives.md) |
| 03 | [Réactivité : ref, reactive, computed, watch](02-reactivite/03-ref-reactive-computed-watch.md) |
| 04 | [Composants, props, emits et slots](03-composants/04-props-emits-slots.md) |
| 05 | [Formulaires, validation et CRUD](04-formulaires/05-formulaires-validation-crud.md) |
| 06 | [API HTTP et états asynchrones](05-api/06-http-fetch-et-etats-asynchrones.md) |
| 07 | [Vue Router](06-vue-router/07-navigation-et-routes.md) |
| 08 | [Pinia](07-pinia/08-etat-partage-pinia.md) |
| 09 | [Composables et architecture](08-composables/09-composables-et-architecture.md) |
| 10 | [TypeScript](09-typescript/10-typescript-avec-vue.md) |
| 11 | [Tests](10-tests/11-tests-vitest-vue-test-utils-playwright.md) |
| 12 | [Accessibilité, sécurité et performance](11-architecture/12-accessibilite-securite-performance.md) |
| 13 | [Nuxt, SSR, SSG et PWA](12-nuxt/13-nuxt-ssr-ssg-pwa.md) |
| 14 | [Laravel et déploiement](13-deploiement/14-integration-laravel-et-deploiement.md) |

## Laboratoires pratiques

- [Index de tous les laboratoires](labs/README.md)
- [LAB 00 — environnement et lecture d'un projet](labs/00-preparer-environnement.md)
- [LAB 09 — routes, Pinia et composables](labs/09-composables-router-pinia.md)
- [LAB 10 — API, TypeScript et tests](labs/10-api-typescript-tests.md)
- [LAB 11 — intégrer Vue à Laravel](labs/11-laravel-final.md)
- [LAB 12 — débogage, accessibilité et performance](labs/12-debugging-accessibilite-performance.md)
- [LAB 13 — Nuxt, PWA et déploiement](labs/13-nuxt-pwa-deploiement.md)

Les laboratoires 01 à 08 sont détaillés dans l'index. Les exercices de synthèse avancés réunissent plusieurs notions déjà étudiées.

## Projets progressifs

- [Cahier des charges — application de restaurant](projets/01-restaurant-cahier-des-charges.md)
- [Liste des projets progressifs](projets/README.md)
- [Projet final — Fondé 44](projets/projet-final-fonde-44.md)
- [Grille d'évaluation de maîtrise](evaluations/grille-maitrise.md)

## Règles de travail

- Tu écris toi-même le code des exercices : le but est d'apprendre à raisonner, pas de recopier.
- Avant de coder, décris le besoin, les données, les actions, les règles et le résultat attendu.
- Suis le cycle : prédire → expérimenter → observer → expliquer → modifier → retester.
- Une fonctionnalité terminée est testée manuellement et, lorsque c'est pertinent, automatiquement.
- Ne confonds pas « ça marche » avec « je comprends pourquoi ça marche ».
- Garde des commits petits et explicites ; travaille sur une branche pour les changements conséquents.
- N'ajoute pas une bibliothèque sans pouvoir expliquer le problème qu'elle résout.
- Si tu bloques, commence par un indice ou une explication ciblée ; après avoir essayé, étudie une correction et explique-la avec tes mots.

## Démarrage rapide

Prérequis : Node.js LTS compatible avec les dépendances, npm, Git et un éditeur comme VS Code.

```bash
node --version
npm --version
npm create vue@latest
cd nom-du-projet
npm install
npm run dev
```

Pour débuter, choisis JavaScript et reporte les outils avancés jusqu'aux modules correspondants. Utilise `npm run build` pour vérifier la compilation de production.

## Calendrier intensif

Le calendrier de 30 jours est un objectif intensif, pas une garantie de maîtrise. La progression dépend de la pratique, de la révision et de ta capacité à expliquer les mécanismes sans modèle.

## Quand la formation est-elle terminée ?

Tu dois pouvoir construire une application de bout en bout, expliquer son architecture, connecter une API, gérer les erreurs, tester les parcours essentiels, corriger un bug et défendre tes décisions techniques sans suivre un tutoriel.

**Note :** ce dépôt fournit le cours et les exercices. Les commandes et tests des projets pratiques doivent être exécutés dans ton environnement local ; les exercices ne sont pas des résultats de tests déjà exécutés.
