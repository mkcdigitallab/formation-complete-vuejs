# Module 10 — TypeScript avec Vue

## Pourquoi
TypeScript ajoute une vérification statique des types. Il aide à détecter certains problèmes avant l'exécution et rend les contrats plus lisibles. Il ne garantit pas à lui seul que les données provenant d'une API sont valides.

## À apprendre
- Types primitifs et tableaux.
- Types d'objets et interfaces.
- Unions discriminées.
- Types optionnels et valeurs nulles.
- Fonctions et types de retour.
- Génériques simples.
- Typage des props et événements.
- Typage des refs et des réponses API.
- Narrowing et vérifications de valeurs inconnues.

## Données externes
Une réponse JSON n'est pas fiable simplement parce qu'on lui attribue un type TypeScript. À la frontière réseau, il faut valider ou vérifier la structure des données à l'exécution lorsque c'est nécessaire.

## Laboratoire
Type les modèles Product, CartItem et Order. Typage des props d'une carte produit, de son événement d'ajout, puis du store panier. Traite une réponse API comme inconnue avant de l'utiliser et explique le contrôle effectué.

## Critères
Tu peux expliquer la différence entre vérification statique et validation à l'exécution.
