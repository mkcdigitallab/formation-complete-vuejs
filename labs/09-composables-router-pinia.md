# LAB 09 — Transformer le catalogue en application multi-pages

**Durée indicative :** 1 à 2 jours.  
**Prérequis :** composants, props/émits, computed et bases d'API.

## Scénario
Un catalogue de plats doit devenir une application multi-pages. Le panier reste accessible partout et la logique ne doit pas être copiée dans plusieurs composants.

## Étape 1 — Concevoir les routes
Prévois :
- / : catalogue ;
- /plats/:id : détail d'un plat ;
- /panier : panier ;
- /historique : historique local ;
- page 404.

Dessine les routes avant d'implémenter. Explique ce qui change lors d'une navigation. Utilise les liens du routeur.

## Étape 2 — Paramètres et navigation
- Le détail récupère l'identifiant depuis l'URL.
- Un identifiant inconnu affiche un état introuvable.
- Une recherche partageable peut être conservée dans les paramètres de requête.
- Vérifie le bouton retour du navigateur.

## Étape 3 — Choisir où vit l'état
Classe les données : menu API, recherche, panier, page courante, session, total calculé.
Pour chaque donnée, justifie si elle est locale, dérivée, dans l'URL, partagée dans Pinia ou détenue par le serveur.

## Étape 4 — Store Pinia
Le store panier doit fournir l'état des lignes, un getter de total et des actions d'ajout, de changement de quantité et de suppression. Empêche les quantités invalides et les dépassements de stock. Regroupe les règles métier plutôt que de les disperser dans plusieurs composants.

## Étape 5 — Persistance
Si elle est utile, restaure le panier depuis localStorage. Gère l'absence de données et un JSON invalide. Ne stocke aucun secret et documente que le navigateur n'est pas la source de vérité serveur.

## Étape 6 — Garde de navigation
Ajoute une route de démonstration protégée par une session simulée. Indique clairement que ce n'est pas une authentification de production. Le backend doit toujours appliquer les autorisations réelles.

## Cas limites
- Le plat n'existe plus.
- Le panier est vide.
- La quantité dépasse le stock.
- L'utilisateur recharge la page.
- Le stockage est corrompu.
- L'utilisateur utilise le bouton retour.
- L'URL mène vers une route inconnue.

## Critères de réussite
- [ ] Les routes fonctionnent.
- [ ] Le panier est partagé entre pages.
- [ ] Le total reste correct.
- [ ] Les identifiants invalides sont gérés.
- [ ] Le choix de chaque emplacement d'état est expliqué.
- [ ] La sécurité ne repose pas uniquement sur l'interface.

## Questions de maîtrise
1. Pourquoi ne pas placer toutes les données dans Pinia ?
2. Pourquoi le total est-il dérivé plutôt que modifié manuellement ?
3. Quand une query string est-elle plus adaptée qu'un store ?
4. Quelle différence entre cacher un lien et sécuriser une ressource ?
5. Comment éviter des quantités incohérentes ?

## Extension
Ajoute un historique de commandes local, puis décris les données qui devront être persistées par un vrai backend.