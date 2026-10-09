# Projet final — Espace client Fondé 44 avec Vue 3

Ce projet s'inspire du besoin réel de Fondé 44. Il sert à apprendre une architecture frontend maintenable et ne doit pas remplacer automatiquement l'application réelle. Travaille d'abord dans un dépôt d'exercice séparé.

## Objectif
Construire une interface mobile-first pour consulter les produits, préparer une commande de démonstration et suivre son état. Prévoir une interface de gestion simple.

## Rôles
- Visiteur/client : consulter produits et informations utiles.
- Client : préparer une commande et consulter ses commandes si le backend d'authentification le permet.
- Gestionnaire : gérer produits et commandes selon les permissions du backend.

Les rôles affichés dans Vue ne prouvent pas l'autorisation. Le backend applique les permissions réelles.

## Données de démonstration
- Fondé : prix de référence 200 FCFA le pot.
- Thiakry : prix de référence 300 FCFA le pot.
- Livraison à partir de 3 pots selon les règles commerciales définies.

Le backend confirme les prix, la disponibilité et les conditions au moment de la commande. Les données envoyées par le navigateur ne sont jamais considérées comme fiables.

## Parcours client
1. Ouvrir la page produits sur téléphone.
2. Consulter produit, prix et disponibilité.
3. Choisir les quantités.
4. Vérifier le résumé avant confirmation.
5. Saisir les informations nécessaires.
6. Envoyer la commande à l'API.
7. Afficher la confirmation retournée par le backend.
8. Consulter l'état de la commande.

Prévois état vide, chargement, erreur réseau et action de réessai.

## Parcours gestionnaire
- Consulter, ajouter et modifier les produits.
- Prévisualiser une image avant l'envoi.
- Consulter les commandes.
- Changer un statut seulement si l'API l'autorise.
- Afficher les erreurs de validation.

Pour l'upload, prévois types de fichiers acceptés, taille maximale, prévisualisation et gestion de l'échec. La validation de sécurité appartient aussi au serveur.

## Architecture suggérée
- pages : écrans associés aux routes ;
- components : éléments visuels réutilisables ;
- composables : logique réutilisable liée à Vue ;
- services : communication HTTP ;
- stores : état partagé nécessaire ;
- types : types TypeScript après étude du module ;
- router : navigation ;
- tests : règles et parcours.

Justifie chaque dossier et évite les fichiers sans responsabilité claire.

## Phases
1. Maquettes et parcours.
2. Modèle de données et règles métier.
3. Interface statique avec données fictives.
4. Réactivité et panier.
5. Composants.
6. Navigation et état partagé.
7. Intégration API.
8. Gestionnaire et upload.
9. Tests, accessibilité et responsive.
10. Build, déploiement et présentation.

## Exigences de qualité
- Mobile-first et utilisable au clavier.
- Texte lisible et messages d'erreur explicites.
- Prix et totaux formatés en FCFA.
- États loading/error/empty/success.
- Gestion des erreurs 401/403/404/422/500.
- Aucun secret dans le frontend.
- Tests des règles de commande et composants essentiels.
- Build de production réussi.
- Documentation d'installation.

## Défis de réflexion
- Quelles données viennent du serveur et lesquelles peuvent rester locales ?
- Comment empêcher la modification du prix dans les outils du navigateur ?
- Comment gérer une commande envoyée deux fois ?
- Que montrer si la connexion est coupée après l'envoi ?
- Comment annoncer une erreur à un lecteur d'écran ?
- Pourquoi une prévisualisation locale ne signifie-t-elle pas que l'image est enregistrée sur le serveur ?

## Livraison
Présente les parcours client et gestionnaire, un test important, un bug corrigé et un schéma du flux de données. Explique le rôle de chaque couche sans lire le code.