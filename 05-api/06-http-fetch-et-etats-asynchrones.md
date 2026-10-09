# Module 06 — API HTTP avec fetch

## Objectifs
Charger des données distantes, traiter les erreurs et rendre l'état de la requête visible.

## Comprendre le flux
Le frontend envoie une requête HTTP. Le serveur répond avec un statut et éventuellement un corps JSON. Une réponse HTTP 404 ou 500 ne déclenche pas automatiquement une exception dans `fetch` : il faut vérifier `response.ok`.

## Les états d'une requête
Prévois au minimum :
- loading : la requête est en cours ;
- success : les données sont disponibles ;
- empty : la requête a réussi mais il n'y a aucun résultat ;
- error : la requête a échoué.

Évite d'afficher une page vide pendant le chargement ou après une erreur.

## async/await
Une fonction asynchrone attend la réponse et traite les données. Entoure le traitement des erreurs réseau et de parsing de manière appropriée. Ne masque pas une erreur avec un tableau vide : cela ferait croire qu'il n'y a aucun produit alors que le serveur est inaccessible.

## Cas réels à considérer
- Réseau indisponible.
- Statut HTTP non réussi.
- JSON invalide.
- Temps de réponse long.
- L'utilisateur change rapidement le filtre et les réponses arrivent dans le désordre.
- Le composant est démonté avant la fin de la requête.

Selon le cas, utilise un contrôleur d'annulation et nettoie les effets asynchrones. Ne place jamais de secret serveur dans le code frontend : tout code livré au navigateur peut être inspecté.

## Laboratoire
1. Charge une liste depuis une API de test.
2. Affiche loading, succès, liste vide et erreur.
3. Ajoute un bouton de rechargement.
4. Affiche un message d'erreur utile sans exposer de données sensibles.
5. Ajoute une recherche déclenchant une nouvelle requête.
6. Gère l'annulation ou les réponses obsolètes.
7. Documente les étapes pour reproduire chaque état.

## Critères
Tu peux expliquer la différence entre erreur réseau, réponse HTTP non réussie et réponse vide.
