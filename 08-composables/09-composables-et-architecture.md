# Module 09 — Composables et architecture

## Qu'est-ce qu'un composable ?
Un composable est une fonction JavaScript, généralement nommée `useQuelqueChose`, qui encapsule une logique réutilisable et peut utiliser la réactivité Vue. Ce n'est pas simplement un composant sans template.

## Quand en créer un ?
Crée un composable quand une logique cohérente est réutilisée ou devient difficile à lire dans le composant. N'extrais pas chaque ligne dans un fichier séparé : l'abstraction doit clarifier le code.

Exemples possibles :
- recherche et filtres ;
- gestion d'une requête HTTP ;
- synchronisation avec localStorage ;
- gestion du panier ;
- écoute d'une préférence d'affichage.

## Responsabilités conseillées
- Page : compose l'écran et coordonne les composants.
- Composant : interface et interactions locales.
- Composable : logique réactive réutilisable.
- Service : communication avec une API ou une dépendance externe.
- Store : état partagé durable entre plusieurs zones de l'application.
- Type/interface : décrit la forme des données.

Ce découpage est un guide, pas une règle rigide. Une petite application n'a pas besoin d'une architecture complexe.

## Laboratoire
Extrais la logique de recherche et de filtrage du catalogue dans un composable. Réutilise-le dans une deuxième liste. Vérifie que chaque écran peut fournir ses propres données sans partager accidentellement son état local.

## Questions
Quelle différence entre composable, composant, service et store ? Quelle logique devrait rester dans le composant ?
