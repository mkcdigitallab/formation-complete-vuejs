# LAB 12 — Débogage, accessibilité et performance

**Durée indicative :** 1 journée.

## Partie A — Débogage intentionnel
Dans ton projet d'entraînement, introduis une erreur à la fois :
1. un import incorrect ;
2. une propriété absente dans les données ;
3. une condition qui cache toujours un bloc ;
4. une clé de liste instable ;
5. une requête API qui retourne un statut d'erreur ;
6. une action qui permet une quantité invalide.

Pour chaque cas, note le symptôme attendu avant de provoquer le bug. Diagnostique-le à l'aide de la console, du terminal et des outils du navigateur. Répare ensuite la cause et vérifie que le parcours normal fonctionne toujours.

## Partie B — Accessibilité pratique
- Chaque champ de formulaire possède un label.
- Tous les boutons et liens sont utilisables au clavier.
- Le focus est visible.
- Le texte et l'arrière-plan ont un contraste suffisant.
- Les erreurs ne sont pas signalées seulement par une couleur.
- Les images informatives ont un texte alternatif utile ; les images décoratives ne perturbent pas la lecture.
- Les titres suivent une hiérarchie cohérente.
- Les états de chargement et les messages importants sont perceptibles.

**Défi :** utilise l'application uniquement au clavier. Note chaque endroit où tu te perds ou ne peux pas agir.

## Partie C — Performance sans optimisation prématurée
1. Identifie une liste volumineuse ou une vue coûteuse.
2. Mesure le comportement avant d'optimiser.
3. Vérifie les dépendances réactives et les recalculs.
4. Étudie le chargement différé des routes.
5. Évite de calculer manuellement une donnée qui peut être dérivée proprement.
6. Vérifie les images, leur taille et leur chargement.
7. Compare les résultats après modification.

N'optimise pas seulement parce qu'un pattern est à la mode : mesure ou identifie un problème concret.

## Critères de réussite
- [ ] Je peux reproduire et diagnostiquer plusieurs bugs.
- [ ] Je peux utiliser l'interface au clavier.
- [ ] Les champs ont des labels et les erreurs sont explicites.
- [ ] Je peux justifier une optimisation à partir d'un problème observé.
- [ ] Les fonctionnalités existantes passent encore les tests.

## Questions
1. Quelle différence entre corriger un symptôme et une cause ?
2. Pourquoi les tests automatiques ne prouvent-ils pas à eux seuls l'accessibilité ?
3. Pourquoi mesurer avant d'optimiser ?
4. Quels éléments doivent être vérifiés côté serveur plutôt que dans Vue ?