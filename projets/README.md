# Projets progressifs

Les projets sont des évaluations pratiques. Commence par définir les données, les rôles, les règles métier et les cas limites. Ne passe pas directement au style visuel avant que le comportement soit clair.

## Projet 1 — Restaurant
Construis un catalogue de plats et un panier local.
**Exigences :** recherche, filtre, tri, quantité disponible, panier, total, état vide, formulaire de gestion des plats.
**Compétences :** directives, réactivité, computed, événements, composants et formulaire.
**Critères :** pas de quantité négative, total correct, clés stables, composants à responsabilité claire.
**Cahier des charges détaillé :** [Projet restaurant](01-restaurant-cahier-des-charges.md).

## Projet 2 — Gestion de stock
Gère produits, catégories, seuil d'alerte et mouvements d'entrée/sortie.
**Exigences :** CRUD, validation, filtres, historique, persistance locale et confirmation avant suppression.
**Compétences :** formulaires, composables, stockage et tests.
**Extensions :** export CSV, pagination et historique des changements.
**Défi métier :** le stock courant doit rester cohérent avec les mouvements enregistrés.

## Projet 3 — Boutique multi-pages
Catalogue, détails, panier, connexion simulée et historique.
**Exigences :** Vue Router, routes dynamiques, Pinia, états de chargement, responsive et erreurs.
**Attention :** la connexion simulée n'est pas une authentification réelle et ne doit jamais être présentée comme sécurisée.

## Projet 4 — Dashboard
Indicateurs, tableaux filtrables, formulaire, préférences et pages de paramètres.
**Exigences :** accessibilité clavier, tests de composants, routes, composants réutilisables et gestion des erreurs.
**Extension :** recherche, pagination, état vide et permissions fournies par une API.

## Projet final — Frontend Vue + API Laravel
Construis un frontend connecté à une API que tu contrôles.
**Exigences minimales :**
- structure pages/components/composables/services/types adaptée au projet ;
- navigation et protection côté interface en complément des autorisations backend ;
- formulaires avec erreurs de validation de l'API ;
- états loading/success/error/empty ;
- pagination et filtres ;
- tests de fonctions, composants et parcours critiques ;
- documentation d'installation et variables d'environnement ;
- build de production réussi ;
- déploiement et README avec captures d'écran.

Pour un scénario métier concret, utilise le [projet final Fondé 44](projet-final-fonde-44.md). Travaille d'abord dans un dépôt d'exercice distinct.

## Présentation et barème
Tu dois montrer un parcours complet, expliquer le flux de données, justifier l'état local/global/serveur, décrire trois cas d'erreur et démontrer les tests. Un projet copié sans explication ne valide pas la formation.

Barème indicatif sur 20 :
- Fonctionnalités et règles métier : 5
- Architecture et séparation des responsabilités : 4
- Cas limites, accessibilité et sécurité : 3
- Tests : 3
- Lisibilité et Git : 2
- Documentation et présentation : 3

## Astuce de progression
Ne construis pas quatre projets superficiels. Termine sérieusement le projet Restaurant, puis construis la boutique multi-pages et le projet final. Chaque nouveau projet doit réutiliser des notions acquises et introduire une difficulté supplémentaire.