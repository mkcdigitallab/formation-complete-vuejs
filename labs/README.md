# Laboratoires — règles et défis

## Comment remettre un laboratoire
Pour chaque défi, fournis :
- l'objectif reformulé ;
- un schéma des données (propriétés et types) ;
- la liste des actions utilisateur ;
- les cas limites ;
- les étapes que tu as réalisées ;
- les erreurs rencontrées et leur diagnostic ;
- une courte explication orale/écrite de tes choix.

## LAB 01 — Catalogue réactif
Données : plats avec id, nom, prix, quantité.
- Afficher la liste et les prix.
- Rechercher par nom.
- Filtrer les ruptures de stock.
- Trier par prix.
- Calculer le nombre de résultats.
- Gérer la liste vide.
**Notions :** tableaux, directives, ref, computed.

## LAB 02 — Panier
- Ajouter un plat.
- Augmenter/diminuer la quantité.
- Retirer un article.
- Calculer sous-total et total.
- Empêcher les quantités invalides.
- Afficher panier vide.
**Notions :** réactivité, computed, événements.

## LAB 03 — Formulaire produit
- Champs nom, prix, stock.
- Validation obligatoire et valeurs positives.
- Messages d'erreur accessibles.
- Création et édition.
- Confirmation de suppression.
**Notions :** v-model, formulaires, CRUD.

## LAB 04 — Composants
- Créer ProductCard et ProductList.
- Transmettre les données avec props.
- Émettre l'événement d'ajout.
- Utiliser un slot pour le titre d'une carte.
- Décrire la responsabilité de chaque composant.
**Notions :** composants, props, emits, slots.

## LAB 05 — Persistance
- Sauvegarder le panier dans localStorage.
- Restaurer au démarrage.
- Gérer une valeur absente ou un JSON invalide.
- Ne pas stocker de secrets dans localStorage.
**Notions :** JSON, cycle de vie, watch.

## LAB 06 — API
- Charger des produits depuis une API de test.
- Afficher loading, succès, erreur et liste vide.
- Désactiver une action pendant le chargement.
- Éviter de laisser une ancienne réponse écraser une nouvelle recherche.
**Notions :** fetch, async/await, états asynchrones.

## LAB 07 — Navigation
- Créer pages Catalogue, Panier et Historique.
- Ajouter des routes dynamiques pour le détail.
- Afficher une page 404.
- Conserver les liens et l'état du panier.
**Notions :** Vue Router, Pinia.

## LAB 08 — Qualité
- Écrire tests des fonctions de calcul.
- Tester une prop et un événement.
- Tester ajout/suppression du panier.
- Documenter comment lancer les tests.
**Notions :** Vitest, Vue Test Utils.

## Auto-évaluation (0 à 2 points par critère)
0 = absent ou ne fonctionne pas ; 1 = fonctionne partiellement ou sans explication ; 2 = fonctionne et je peux expliquer.
- Fonctionnalités demandées
- Cas limites
- Découpage des responsabilités
- Lisibilité
- Accessibilité
- Tests
- Explication des décisions
**Objectif :** au moins 11/14, sans zéro sur fonctionnalités ou explication.
