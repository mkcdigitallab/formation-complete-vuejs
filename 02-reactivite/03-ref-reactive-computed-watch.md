# Module 03 — Maîtriser la réactivité : ref, reactive, computed et watch

## Objectifs

À la fin de ce module, tu dois pouvoir expliquer ce qu'est l'état d'une interface, distinguer une donnée source d'une valeur calculée, choisir entre `ref` et `reactive`, comprendre où utiliser `.value`, choisir entre `computed`, une fonction et un watcher, et diagnostiquer les erreurs courantes.

## 1. Pourquoi la réactivité existe-t-elle ?

L'état d'une application est l'ensemble des données qui décrivent sa situation actuelle. Pour le restaurant, il peut s'agir des plats, des quantités disponibles, de la recherche saisie et du panier.

L'interface est une représentation de cet état. Si le prix ou la quantité change, l'affichage qui dépend de cette donnée doit suivre le changement.

Vue ne suit pas automatiquement toutes les variables JavaScript. Une variable ordinaire ne devient pas réactive simplement parce qu'elle est déclarée dans `<script setup>`. Il faut utiliser les mécanismes réactifs appropriés.

Trois notions à distinguer :
- **Donnée source** : valeur conservée et modifiée directement, par exemple la quantité sélectionnée.
- **Valeur dérivée** : résultat calculé à partir de données sources, par exemple le prix total du panier.
- **Effet secondaire** : action qui agit en dehors du simple calcul d'une valeur, par exemple sauvegarder le panier ou envoyer une requête.

Cette distinction aide à choisir le bon outil.

## 2. ref : une référence réactive

`ref(valeurInitiale)` crée une référence réactive. La valeur est conservée dans sa propriété `.value`.

```vue
<script setup>
import { ref } from 'vue'

const compteur = ref(0)
</script>

<template>
  <p>Compteur : {{ compteur }}</p>
  <button @click="compteur++">Ajouter un</button>
</template>
```

Explication :
1. `ref` est importé depuis Vue.
2. `ref(0)` crée une référence dont la valeur initiale est zéro.
3. Dans le script, la valeur se lit et se modifie avec `compteur.value`.
4. Dans le template, Vue déballe automatiquement une ref de premier niveau, donc on utilise `compteur` sans écrire `.value`.
5. Lorsque la valeur change, Vue actualise le texte qui en dépend.

Dans un gestionnaire de template, une expression telle que `compteur++` bénéficie de ce déballage du template. Dans une fonction JavaScript déclarée dans le script, il faut généralement écrire `compteur.value++`.

### Pourquoi .value existe-t-il ?

Une variable déclarée avec `const compteur = ref(0)` contient un objet référence. Le nombre est conservé dans sa propriété `.value`. Le code JavaScript doit donc accéder à cette propriété. Vue simplifie cet accès dans les templates pour éviter de répéter `.value` dans l'interface.

N'en déduis pas que `.value` est inutile : sa nécessité dépend du contexte. Dans le script, garde la règle de base : une ref se lit ou se modifie via `.value`.

### Quand utiliser ref ?

`ref` fonctionne pour un nombre, une chaîne, un booléen, mais aussi pour un objet. C'est un choix polyvalent, notamment quand tu veux remplacer la valeur entière ou conserver une référence réactive facile à identifier.

## 3. reactive : rendre un objet réactif

`reactive(objet)` crée un proxy réactif. Le proxy permet à Vue de suivre les lectures et les modifications des propriétés.

```vue
<script setup>
import { reactive } from 'vue'

const formulaire = reactive({
  nom: '',
  prix: 0,
  stock: 0
})
</script>

<template>
  <p>Nom saisi : {{ formulaire.nom }}</p>
</template>
```

Ici, `formulaire` est directement le proxy. On accède à `formulaire.nom`, pas à `formulaire.value.nom`.

### Limites importantes de reactive

Le proxy doit rester la référence utilisée pour les accès réactifs. Si tu réassignes la variable qui le contient avec un nouvel objet, tu peux perdre la relation réactive attendue. La destructuration demande également de l'attention : extraire une propriété primitive dans une variable indépendante ne crée pas automatiquement une liaison réactive avec la propriété du proxy.

C'est pourquoi `reactive` est utile lorsque tu travailles naturellement avec un objet et ses propriétés, mais `ref` est souvent plus simple lorsqu'une valeur doit être remplacée ou lorsque tu veux une règle uniforme.

## 4. Comment choisir entre ref et reactive ?

Il n'existe pas une règle selon laquelle l'un serait toujours meilleur que l'autre.

Utilise `ref` lorsque :
- tu gères une valeur primitive ;
- tu veux remplacer la valeur entière facilement ;
- tu souhaites un style cohérent pour des valeurs de nature différente.

Utilise `reactive` lorsque :
- tu manipules directement les propriétés d'un objet structuré ;
- tu n'as pas besoin de remplacer souvent la référence entière ;
- le code est plus clair sans `.value`.

Évite de mélanger les deux sans raison. Le meilleur choix est celui que tu peux expliquer et maintenir.

## 5. computed : calculer une valeur dérivée

Un prix total dépend des lignes du panier, du prix de chaque plat et de la quantité commandée. Stocker manuellement le total en plus de ces données crée un risque : si une quantité change et que le total n'est pas mis à jour, les données se contredisent.

Une propriété calculée exprime cette dépendance.

```vue
<script setup>
import { computed, ref } from 'vue'

const prix = ref(2000)
const quantite = ref(2)
const total = computed(() => prix.value * quantite.value)
</script>

<template>
  <p>Total : {{ total }} FCFA</p>
</template>
```

Décomposition :
- `prix` et `quantite` sont des données sources ;
- `computed` définit le calcul du total ;
- le calcul lit les valeurs des refs avec `.value` parce qu'il se trouve dans JavaScript ;
- le template affiche `total`, qui est déballé ;
- si le prix ou la quantité change, le total est recalculé lorsqu'il est nécessaire et l'interface est actualisée.

Une valeur `computed` est mise en cache selon ses dépendances réactives. Si rien dont elle dépend n'a changé, Vue peut réutiliser le résultat. Elle doit normalement rester sans effet secondaire : elle calcule une valeur, elle ne sauvegarde pas des données et ne lance pas une requête.

## 6. computed ou fonction ?

Une fonction peut également calculer un total. La différence principale est le moment où le calcul est exécuté et le rôle que l'outil exprime.

- Une fonction est appelée explicitement à chaque fois que tu l'invoques.
- Une valeur `computed` représente une donnée dérivée et met son résultat en cache jusqu'à ce que ses dépendances changent.

Pour afficher le total du panier dans plusieurs endroits, `computed` décrit bien une valeur qui dépend du panier. Pour calculer un résultat ponctuel après une action précise, une fonction est souvent plus appropriée.

Ne choisis pas `computed` uniquement parce que le code contient une multiplication : choisis-le parce que tu veux représenter une valeur dérivée réactive.

## 7. watch : observer une source explicite

`watch` surveille une source réactive donnée et lance un callback quand cette source change. Il est utile lorsqu'un changement doit déclencher un effet secondaire.

Exemples de besoins :
- sauvegarder une préférence dans `localStorage` ;
- déclencher une recherche API lorsqu'un terme change ;
- synchroniser une ressource externe ;
- réagir à un changement avec accès à l'ancienne et à la nouvelle valeur.

Un watcher ne doit pas être utilisé pour maintenir une valeur calculée simple. Si le total dépend du prix et de la quantité, `computed` est plus direct et évite de conserver un total qui pourrait se désynchroniser.

## 8. watchEffect : détecter automatiquement les dépendances lues

`watchEffect` exécute immédiatement son callback et suit automatiquement les dépendances réactives lues pendant son exécution synchrone. Lorsque ces dépendances changent, il réexécute le callback.

Différence essentielle :
- `watch` : tu indiques explicitement la source à surveiller ;
- `watchEffect` : Vue détecte les dépendances à partir des lectures effectuées dans l'effet.

Le caractère automatique peut être pratique, mais il peut rendre les dépendances moins visibles. Choisis l'outil qui rend le comportement le plus clair. Si tu lances une requête réseau, pense aux erreurs, au nettoyage et aux réponses qui peuvent arriver dans le désordre.

## 9. Erreurs fréquentes

- Oublier `.value` en JavaScript : tu manipules la ref elle-même au lieu de sa valeur.
- Écrire `.value` partout dans le template : les refs de premier niveau sont généralement déballées automatiquement.
- Croire qu'une variable ordinaire est réactive : déclarer une variable dans `script setup` ne suffit pas.
- Maintenir le total à la main : une modification peut oublier de le recalculer.
- Utiliser un watcher pour tout : certains effets devraient être des valeurs calculées.
- Modifier directement une valeur calculée en lecture seule : modifie les données sources.
- Déstructurer une propriété de `reactive` puis s'attendre à une liaison automatique : la variable extraite peut ne plus suivre le proxy.
- Déclencher des requêtes sans gérer les anciennes réponses : une réponse lente peut écraser un résultat plus récent.

## Laboratoire — Panier de restaurant

Construis toi-même un panier à partir d'un catalogue de plats.

1. Déclare les données du catalogue.
2. Représente les quantités sélectionnées avec un état réactif.
3. Affiche le nombre total d'articles.
4. Calcule le total avec une valeur dérivée.
5. Permets d'ajouter ou retirer un article.
6. Empêche une quantité négative et respecte les limites de stock.
7. Affiche un état vide.
8. Ajoute une préférence de panier sauvegardée dans le navigateur et justifie si un watcher est utile.
9. Recharge la page et vérifie le comportement de la persistance.
10. Explique quelles données sont sources, quelle valeur est dérivée et quel comportement est un effet secondaire.

## Questions de compréhension

1. Pourquoi une variable JavaScript ordinaire ne suffit-elle pas toujours pour une interface réactive ?
2. Pourquoi utilise-t-on `.value` dans le script mais pas généralement dans le template ?
3. Dans quels cas choisirais-tu `ref` plutôt que `reactive` ?
4. Quelle différence entre donnée source et valeur dérivée ?
5. Pourquoi le total d'un panier est-il généralement un bon candidat pour `computed` ?
6. Quelle différence entre `computed`, une fonction et `watch` ?
7. Dans quel cas `watchEffect` peut-il être utile ?
8. Pourquoi faut-il se méfier de la destructuration d'un objet réactif ?

## Critères de réussite

Tu peux expliquer les mécanismes sans regarder le cours, construire le panier et justifier chaque choix. Si tu sais seulement reproduire l'exemple mais pas expliquer ce qui déclenche la mise à jour, reviens à la section sur la réactivité.
