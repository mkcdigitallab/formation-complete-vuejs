# Module 07 — Vue Router

## Rôle
Vue Router associe des URL à des composants de page et gère la navigation d'une application Vue. Il ne remplace pas les contrôles d'accès du backend.

## Concepts
- Route : règle qui associe un chemin à une page.
- RouterLink : lien de navigation.
- RouterView : emplacement où s'affiche la page courante.
- Paramètre de route : partie variable du chemin, par exemple un identifiant.
- Query string : paramètres de recherche dans l'URL.
- Route imbriquée : page enfant rendue dans le layout parent.
- Route 404 : réponse visuelle lorsqu'aucune route ne correspond.
- Guard : fonction qui peut autoriser, rediriger ou interrompre une navigation.

## Organisation conseillée
Sépare les pages de niveau route des composants réutilisables. Les layouts contiennent les zones communes, par exemple navigation et pied de page.

## Navigation privée
Un guard frontend améliore l'expérience, mais ne protège pas les données à lui seul. Le serveur doit vérifier les droits à chaque requête sensible. Ne mets pas de mot de passe ou de secret dans le routeur.

## Laboratoire
Construis les pages Catalogue, Détail produit, Panier, Historique et 404.
- Utilise un paramètre pour le détail d'un produit.
- Utilise une query string pour une recherche partageable.
- Ajoute des liens de retour.
- Crée un layout commun.
- Simule une session puis protège une page côté navigation.
- Explique pourquoi le backend doit quand même vérifier les autorisations.

## Questions
Quand choisir un paramètre de route plutôt qu'une query string ? Qu'est-ce que RouterView affiche ? Pourquoi un guard n'est-il pas une frontière de sécurité suffisante ?
