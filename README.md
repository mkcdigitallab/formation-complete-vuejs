# Formation complète Vue.js — du débutant au développeur autonome

> Objectif : apprendre Vue 3 et son écosystème par la compréhension, la pratique, le débogage et des projets progressifs. La formation vise l'autonomie, pas la copie de solutions.

## Démarrer dans le bon ordre

1. Lis le [plan de formation](PLAN-DE-FORMATION.md).
2. Suis le [guide de l'apprenant](GUIDE-APPRENANT.md).
3. Réalise [LAB 00 : préparer l'environnement](labs/00-preparer-environnement.md).
4. Étudie les modules dans l'ordre et coche [le suivi de progression](SUIVI-DE-PROGRESSION.md).
5. Utilise la [méthode de résolution de problèmes](METHODE-DE-RESOLUTION.md) dès que tu bloques.
6. Consulte les [astuces et pièges courants](ASTUCES-ET-PIEGES.md) après avoir essayé de diagnostiquer.
7. Termine les projets et les évaluations sans suivre une solution pas à pas.

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

- [Tous les laboratoires et règles de rendu](labs/README.md)
- [LAB 00 — environnement et lecture d'un projet](labs/00-preparer-environnement.md)
- [LAB 09 — routes, Pinia et composables](labs/09-composables-router-pinia.md)
- [LAB 10 — API, TypeScript et tests](labs/10-api-typescript-tests.md)
- [LAB 11 — intégrer Vue à Laravel](labs/11-laravel-final.md)

Les laboratoires 01 à 08 sont détaillés dans l'index des laboratoires. Les numéros avancés sont des exercices de synthèse qui réunissent plusieurs notions.

## Projets progressifs

- [Cahier des charges complet — restaurant](projets/01-restaurant-cahier-des-charges.md)
- [Liste des projets progressifs](projets/README.md)
- [Projet final contextualisé — Fondé 44](projets/projet-final-fonde-44.md)
- [Grille d'évaluation de maîtrise](evaluations/grille-maitrise.md)

## Règles de travail

- Tu écris toi-même le code des exercices.
- Avant de coder, décris le besoin, les données, les actions et le résultat attendu.
- Prédire → expérimenter → observer → expliquer → modifier → retester.
- Une fonctionnalité terminée est testée manuellement et, quand c'est pertinent, automatiquement.
- Ne confonds pas « ça marche » avec « je comprends pourquoi ça marche ».
- Garde les commits petits et explicites ; ne travaille pas directement sur main pour les projets.
- N'ajoute pas une bibliothèque sans pouvoir expliquer le problème qu'elle résout.
- Si tu demandes de l'aide, demande d'abord un indice. La correction complète vient après une tentative.

## Démarrage rapide

Prérequis recommandés : Node.js LTS compatible avec les dépendances, npm, Git et VS Code.

Créer un projet avec l'outil officiel :

    npm create vue@latest
    cd nom-du-projet
    npm install
    npm run dev

Choisis les options selon le module étudié. Pour le premier exercice, commence simplement en JavaScript et active les outils avancés lorsque le cours les aborde.

## Calendrier intensif

Le calendrier de 30 jours est un objectif intensif, pas une garantie de maîtrise. Travaille chaque jour avec une réalisation concrète et reviens sur les notions que tu ne sais pas expliquer.

## Quand la formation est-elle terminée ?

Tu dois pouvoir construire une application de bout en bout, expliquer son architecture, connecter une API, gérer les états d'erreur, tester les parcours essentiels, corriger un bug et présenter tes décisions sans suivre un tutoriel. La [grille de maîtrise](evaluations/grille-maitrise.md) t'aide à vérifier tes acquis.

**Important :** ce dépôt est une formation documentaire avec des exercices. Les commandes, applications et tests de tes projets doivent être exécutés dans ton environnement local ; les laboratoires ne sont pas des résultats de tests déjà exécutés.