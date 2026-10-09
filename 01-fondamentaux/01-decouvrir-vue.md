# Module 01 — Découvrir Vue 3 et son projet

## Objectifs
- Expliquer le rôle de Vue.
- Créer un projet Vue 3 avec Vite.
- Identifier les fichiers importants.
- Comprendre le cycle modification → compilation/développement → navigateur.

## 1. Qu'est-ce que Vue ?
Vue est un framework JavaScript pour construire des interfaces utilisateur. On décrit l'interface à partir de données et Vue met à jour le DOM lorsque les données réactives changent. Vue ne remplace ni HTML, ni CSS, ni JavaScript : il organise leur usage pour construire des interfaces.

## 2. Initialiser un projet
Prérequis : Node.js LTS et npm installés.

```bash
node --version
npm --version
npm create vue@latest
cd nom-du-projet
npm install
npm run dev
```

Choisis un nom simple. Pour le tout premier passage, tu peux refuser TypeScript, Router, Pinia et les outils de test afin de comprendre le socle. Ils seront ajoutés/étudiés dans les modules correspondants.

## 3. Repères dans le projet
- `package.json` : scripts et dépendances du projet.
- `index.html` : document HTML d'entrée.
- `src/main.js` : crée l'application Vue et la monte dans la page.
- `src/App.vue` : composant racine.
- `src/components/` : composants réutilisables.
- `public/` : ressources servies telles quelles.
- `node_modules/` : dépendances installées, ne pas modifier manuellement.
- `dist/` : résultat de production généré par le build.

Un fichier `.vue` est un Single-File Component (SFC). Il peut contenir `<template>`, `<script setup>` et `<style>`.

## 4. Développement et production
`npm run dev` démarre un serveur de développement avec rechargement rapide. `npm run build` vérifie et produit le bundle de production dans `dist/`. Le serveur de développement n'est pas le serveur de production.

## Laboratoire
1. Crée le projet.
2. Lance le serveur et ouvre l'adresse affichée.
3. Repère les fichiers listés ci-dessus.
4. Change le titre visible du composant racine.
5. Observe le navigateur après sauvegarde.
6. Lance `npm run build` et vérifie que le build termine sans erreur.
7. Explique le rôle de `main.js`, `App.vue` et `package.json` sans lire le cours.

## Questions de contrôle
1. Vue est-il un langage de programmation ?
2. Quel fichier monte l'application ?
3. Quelle différence entre `dev` et `build` ?
4. Pourquoi ne modifie-t-on pas `node_modules` directement ?

## Critères de réussite
Tu peux créer et lancer un projet neuf, retrouver les fichiers d'entrée, modifier l'interface et expliquer le résultat.
