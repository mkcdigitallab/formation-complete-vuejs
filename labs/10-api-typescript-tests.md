# LAB 10 — Fiabiliser une interface connectée à une API

**Durée indicative :** 1 à 2 jours.

## Partie A — Contrat API
Avant de coder, documente pour chaque endpoint : URL, méthode, paramètres, corps de requête, réponse, statuts, forme des erreurs et pagination. Ne suppose pas que la réponse contient toujours les propriétés attendues.

## Partie B — États d'interface
Pour le catalogue, prévois : attente, chargement, succès avec résultats, succès sans résultat et erreur avec possibilité de réessayer. Une liste vide n'est pas une erreur réseau.

## Partie C — Couche de service
Isole les appels HTTP dans un module de service lorsque cela évite de répéter la même logique. Le service vérifie les statuts HTTP, transforme les réponses en données exploitables et propage une erreur gérable par l'interface. Évite une architecture complexe si elle n'apporte pas de clarté.

## Partie D — Recherche concurrente
1. Lance une recherche lente.
2. Lance rapidement une autre recherche.
3. Observe l'ordre des réponses.
4. Empêche la réponse ancienne de remplacer le résultat récent.
Étudie AbortController et le nettoyage d'un watch.

## Partie E — TypeScript
Ajoute des types pour produit, ligne de panier, réponse API, erreur de validation et props. Étudie les unions pour représenter des états incompatibles. Évite any sans raison : un type doit aider à prévenir une erreur réelle.

## Partie F — Tests
Écris des tests pour :
1. calculer un total ;
2. refuser une quantité invalide ;
3. afficher un état vide ;
4. émettre un événement d'ajout ;
5. afficher les erreurs de validation ;
6. gérer une réponse API en échec ;
7. vérifier un parcours critique avec un test navigateur si l'environnement le permet.

Un test utile vérifie un comportement observable plutôt qu'un détail interne sans importance.

## Critères d'acceptation
- [ ] Les statuts HTTP d'erreur sont traités.
- [ ] Les états de chargement sont visibles.
- [ ] Les erreurs sont compréhensibles et réessayables.
- [ ] Les types sont précis et utiles.
- [ ] Les règles métier critiques sont testées.
- [ ] Les tests ne dépendent pas de leur ordre.
- [ ] Le build et les tests passent localement.

## Analyse après test
Pour chaque test, explique le risque couvert, le bug qu'il aurait détecté et pourquoi un test manuel ne suffit pas toujours.

## Extension
Ajoute une pagination et compare la pagination côté client à celle côté serveur.