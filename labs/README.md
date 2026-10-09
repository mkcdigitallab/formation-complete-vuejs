# Laboratoires Vue 3 — apprendre en construisant

Les laboratoires sont progressifs. N'essaie pas de les terminer en copiant une solution : ton objectif est de pouvoir refaire l'exercice avec des exigences légèrement différentes.

## Comment travailler sur chaque laboratoire

1. Reformule le besoin en une ou deux phrases.
2. Note les données, leurs propriétés et leurs types.
3. Liste les actions utilisateur et le résultat attendu.
4. Écris les cas limites avant de coder.
5. Construis la plus petite version fonctionnelle.
6. Teste, lis les erreurs et corrige une hypothèse à la fois.
7. Explique les choix sans regarder le code.
8. Fais un commit cohérent et écris un court bilan.

## Parcours

### LAB 00 — Environnement
[Consignes détaillées](00-preparer-environnement.md). Créer un projet, reconnaître les fichiers, comprendre Node, npm, Vite et Git.

### LAB 01 — Catalogue réactif
Données : plats avec id, nom, prix, quantité.
- Afficher la liste et les prix.
- Rechercher par nom.
- Filtrer les ruptures de stock.
- Trier par prix.
- Calculer le nombre de résultats.
- Gérer la liste vide.
- Vérifier que filtrer ne modifie pas la liste d'origine.
**Notions :** tableaux, directives, ref, computed.

### LAB 02 — Panier
- Ajouter un plat.
- Augmenter et diminuer la quantité.
- Retirer un article.
- Calculer sous-total et total.
- Empêcher les quantités invalides et les dépassements de stock.
- Afficher un panier vide.
**Notions :** réactivité, computed, événements.

### LAB 03 — Formulaire produit
- Champs nom, prix et stock.
- Validation des champs obligatoires et des valeurs positives.
- Messages d'erreur accessibles.
- Création et édition.
- Confirmation de suppression.
- Préserver les données si la validation échoue.
**Notions :** v-model, formulaires, CRUD.

### LAB 04 — Composants
- Créer ProductCard et ProductList.
- Transmettre les données avec props.
- Émettre l'événement d'ajout.
- Utiliser un slot pour le titre d'une carte.
- Décrire la responsabilité de chaque composant.
- Vérifier que l'enfant ne modifie pas directement la prop.
**Notions :** composants, props, emits, slots.

### LAB 05 — Persistance
- Sauvegarder le panier dans localStorage.
- Restaurer au démarrage.
- Gérer une valeur absente ou un JSON invalide.
- Tester ce qui se passe après rechargement.
- Ne pas stocker de secrets.
**Notions :** JSON, cycle de vie, watch.

### LAB 06 — API
- Charger des produits depuis une API de test.
- Afficher chargement, succès, erreur et liste vide.
- Désactiver une action pendant le chargement.
- Vérifier les statuts HTTP.
- Éviter qu'une ancienne réponse remplace une nouvelle recherche.
**Notions :** fetch, async/await, états asynchrones.

### LAB 07 — Navigation
- Créer pages Catalogue, Panier et Historique.
- Ajouter des routes dynamiques pour le détail.
- Afficher une page 404.
- Conserver les liens et l'état du panier.
- Vérifier le bouton retour.
**Notions :** Vue Router, Pinia.

### LAB 08 — Qualité
- Tester les fonctions de calcul.
- Tester une prop et un événement.
- Tester ajout et suppression du panier.
- Tester un état vide et une erreur.
- Documenter comment lancer les tests.
**Notions :** Vitest, Vue Test Utils.

### LAB 09 — Application multi-pages
[Consignes détaillées](09-composables-router-pinia.md). Router, choix de l'état, Pinia, persistance et routes de démonstration.

### LAB 10 — API et tests
[Consignes détaillées](10-api-typescript-tests.md). États asynchrones, concurrence des requêtes, TypeScript et tests.

### LAB 11 — Intégration Laravel
[Consignes détaillées](11-laravel-final.md). Contrat API, configuration, erreurs de validation, sécurité et livraison.

## Tests manuels à répéter
Pour chaque fonctionnalité, teste au moins un cas normal, un cas limite et un cas d'échec. Exemples : liste vide, identifiant absent, saisie invalide, réseau coupé, double clic et rechargement de page.

## Rendu d'un laboratoire
Fournis :
- objectif reformulé ;
- modèle des données ;
- actions utilisateur ;
- cas limites ;
- capture ou description du résultat ;
- erreurs rencontrées et diagnostic ;
- commandes et tests exécutés ;
- explication de tes décisions.

## Auto-évaluation (0 à 2 points par critère)
0 = absent ou cassé ; 1 = partiel ou impossible à expliquer ; 2 = fonctionne et tu peux l'expliquer.
- Fonctionnalités demandées
- Cas limites
- Responsabilités des composants
- Lisibilité
- Accessibilité
- Tests
- Explication des décisions

**Objectif :** au moins 11/14, sans zéro sur les fonctionnalités ou l'explication.