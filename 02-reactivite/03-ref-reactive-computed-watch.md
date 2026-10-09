# Module 03 — Réactivité : ref, reactive, computed et watch

## Le principe
La réactivité permet à Vue de suivre certaines données et de mettre à jour les parties de l'interface qui en dépendent. Toutes les variables JavaScript ne deviennent pas automatiquement réactives.

## ref()
`ref(valeur)` crée un conteneur réactif avec une propriété `.value`. Dans le JavaScript du composant, on lit et modifie généralement `.value`. Dans le template, Vue déballe généralement la ref de premier niveau automatiquement.

Utilise `ref` pour les valeurs primitives et aussi pour les objets lorsque tu veux une référence réactive simple.

## reactive()
`reactive(objet)` crée un proxy réactif d'un objet. On accède directement à ses propriétés. Il convient aux objets dont on souhaite suivre les propriétés. Évite de remplacer la référence entière et sois prudent en destructurant ses propriétés : une variable destructurée n'est pas automatiquement une liaison réactive au proxy.

## Comment choisir ?
- `ref` : choix polyvalent, valeur primitive, remplacement simple de la valeur.
- `reactive` : objet structuré dont on utilise directement les propriétés.
- Ne choisis pas en fonction d'une règle magique : garde un style cohérent et compréhensible.

## computed()
Une propriété calculée exprime une valeur dérivée d'autres données réactives, par exemple le total du panier. Elle est mise en cache et recalculée lorsque ses dépendances changent. Elle doit normalement rester sans effet secondaire.

## watch() et watchEffect()
- `watch` surveille explicitement une source et permet de comparer les valeurs avant/après.
- `watchEffect` exécute une fonction et détecte les dépendances réactives qu'elle lit synchroniquement.
Utilise-les pour les effets secondaires : enregistrer une préférence, synchroniser une API, réagir à un changement. N'utilise pas un watcher pour remplacer un simple calcul dérivé qui relève de `computed`.

## Laboratoire — Panier
À partir d'une liste de plats :
1. Stocke les quantités sélectionnées dans une donnée réactive.
2. Calcule le nombre total d'articles avec `computed`.
3. Calcule le prix total avec `computed`.
4. Permets d'ajouter et de retirer un article.
5. Refuse les quantités négatives.
6. Observe ce qui change automatiquement quand les données sont modifiées.
7. Ajoute ensuite une préférence de panier sauvegardée dans le navigateur et justifie si un watcher est pertinent.

## Erreurs fréquentes
- Oublier `.value` dans le JavaScript lorsqu'on manipule une ref.
- Penser que `.value` est toujours nécessaire dans un template.
- Modifier une valeur calculée au lieu de modifier ses sources.
- Utiliser `watch` pour chaque calcul.
- Déstructurer un objet réactif et s'attendre à ce que chaque variable reste liée au proxy.

## Questions
Explique avec tes propres mots : donnée source, valeur dérivée, effet secondaire. Donne un exemple de chaque.
