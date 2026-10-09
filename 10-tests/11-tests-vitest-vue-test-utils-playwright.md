# Module 11 — Tester une application Vue

## Pourquoi tester ?
Un test vérifie un comportement précis et aide à prévenir les régressions. Les tests ne remplacent pas le jugement : ils doivent être lisibles, utiles et entretenus.

## Niveaux de test
- Unitaire : une fonction ou une unité isolée, par exemple le calcul d'un total.
- Composant : rendu, props, événements et interactions utilisateur.
- End-to-end : parcours de bout en bout dans un navigateur.

Outils courants de l'écosystème : Vitest, Vue Test Utils et Playwright. Lis leur documentation officielle pour la configuration correspondant aux versions utilisées.

## Quoi tester ?
- Calcul du total et arrondis éventuels.
- Quantités limites.
- Validation des formulaires.
- Affichage de la liste vide.
- Propagations d'événements.
- États loading/error/success.
- Parcours ajouter au panier puis vérifier le total.
- Navigation vers une route inexistante.

## Bonnes pratiques
Teste le comportement observable plutôt que les détails internes. Évite les tests qui échouent à chaque petit changement de structure sans raison fonctionnelle. Un test doit avoir une intention claire et des données explicites.

## Laboratoire
1. Écris des tests unitaires pour les calculs du panier.
2. Teste un composant qui reçoit une prop et émet un événement.
3. Teste le formulaire invalide puis valide.
4. Teste le parcours principal dans le navigateur.
5. Introduis volontairement une régression et vérifie que le test la détecte.

## Critères
Tu sais expliquer ce que chaque test garantit et ce qu'il ne garantit pas.
