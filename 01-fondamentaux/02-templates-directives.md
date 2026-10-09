# Module 02 — Comprendre le template et les directives Vue

## Objectifs

À la fin du module, tu dois pouvoir expliquer comment Vue affiche des données, comment il remplit un attribut HTML à partir d'une variable, comment il réagit à un événement et comment il décide quels éléments afficher. Tu dois aussi savoir choisir entre les directives sans les confondre.

## 1. Le template : HTML enrichi par Vue

Dans un composant Vue, le bloc `<template>` décrit la structure visible. Il ressemble au HTML, mais Vue reconnaît aussi des syntaxes particulières : interpolation, directives et expressions. Le template est compilé par Vue ; il ne faut pas le confondre avec un fichier HTML indépendant.

Le template décrit l'interface souhaitée. Le script déclare les données et les comportements. Le CSS gère la présentation. Cette séparation permet de comprendre quelle partie du code est responsable de quoi.

## 2. Interpolation : afficher une valeur dans le texte

La syntaxe `{{ expression }}` affiche le résultat d'une expression JavaScript dans le contenu textuel.

```vue
<template>
  <h2>{{ nomPlat }}</h2>
  <p>Prix : {{ prix }} FCFA</p>
</template>

<script setup>
const nomPlat = 'Mafé'
const prix = 2500
</script>
```

Décomposition :
- `nomPlat` et `prix` sont des variables JavaScript ;
- les doubles accolades indiquent à Vue d'évaluer l'expression ;
- le résultat est affiché dans le texte de la page.

Dans cet exemple, les variables sont constantes : on illustre l'affichage, pas encore la réactivité. Les données réactives seront étudiées au module 03.

Une expression doit produire une valeur. Les expressions simples sont adaptées au template ; un calcul complexe ou une règle métier doit être nommé dans le script, souvent avec `computed`.

## 3. Attribut HTML fixe ou dynamique : comprendre v-bind

Un attribut HTML fournit une information à un élément. Par exemple, `src` indique la source d'une image, `href` indique la destination d'un lien et `disabled` indique si un bouton est désactivé.

### Cas A — Valeur fixe

```html
<img src="/images/mafe.jpg" alt="Bol de mafé">
```

Le navigateur reçoit le texte `/images/mafe.jpg` comme valeur de l'attribut `src`. Cette valeur est écrite directement dans le template.

### Cas B — Valeur fournie par une variable Vue

Supposons que le script contienne une variable `imagePlat` dont la valeur est `/images/mafe.jpg`. Si tu écris `src="imagePlat"`, le navigateur reçoit le texte littéral `imagePlat`. Il ne devine pas que ce mot est le nom d'une variable JavaScript.

Pour demander à Vue d'évaluer la variable, on écrit `:src="imagePlat"`. Vue lit la valeur de la variable et la lie à l'attribut `src`.

Les écritures suivantes sont équivalentes :
- `v-bind:src="imagePlat"`
- `:src="imagePlat"`

Le deux-points est simplement le raccourci de `v-bind:`.

| Écriture | Interprétation |
|---|---|
| `src="/images/mafe.jpg"` | Valeur fixe écrite directement. |
| `src="imagePlat"` | Texte littéral `imagePlat`, pas la variable. |
| `:src="imagePlat"` | Évalue l'expression JavaScript `imagePlat`. |
| `v-bind:src="imagePlat"` | Même comportement que `:src`. |
| `:src="dossier + '/' + fichier"` | Évalue une expression JavaScript qui construit une valeur. |

### Pourquoi les guillemets ne suffisent-ils pas ?

Dans un attribut HTML ordinaire, ce qui est entre guillemets est une valeur textuelle. Vue a besoin d'un signal explicite pour distinguer une valeur écrite directement d'une expression JavaScript. `: ` (sans espace) ou `v-bind:` fournit ce signal.

Utilise `:href` pour un lien dont la destination vient d'une donnée, `:alt` pour une description dynamique, `:class` pour des classes calculées ou `:disabled` pour activer/désactiver un bouton à partir d'une condition. N'ajoute pas `:` à tous les attributs : utilise-le quand la valeur dépend d'une expression.

Attention : l'expression doit exister et fournir une valeur appropriée. Si le chemin d'une image est incorrect, la liaison peut fonctionner correctement tout en affichant une image cassée : le problème est alors le chemin, pas forcément `v-bind`.

## 4. Événements : v-on et @

Un événement est une action ou un changement détectable, comme un clic, une saisie clavier ou l'envoi d'un formulaire. Pour écouter un clic, Vue permet d'écrire `v-on:click` ou son raccourci `@click`.

Un gestionnaire d'événement est la fonction exécutée en réponse. Dans une application, un bouton « Ajouter au panier » doit déclencher une action clairement nommée. Il ne doit pas simplement modifier arbitrairement le DOM : les données Vue doivent représenter l'état de l'application.

Les deux syntaxes sont équivalentes :
- `v-on:click="ajouterAuPanier"`
- `@click="ajouterAuPanier"`

Quand le gestionnaire est une fonction déjà déclarée, on peut généralement référencer son nom. Quand on écrit une expression d'appel avec des arguments, il faut comprendre quand la fonction est appelée et quelles valeurs lui sont transmises.

### Modificateurs

Les modificateurs indiquent à Vue un traitement courant de l'événement. Par exemple, `@submit.prevent` empêche le comportement natif de soumission qui rechargerait normalement la page. Le modificateur `.stop` arrête la propagation de l'événement. Ne les ajoute pas automatiquement : utilise-les lorsqu'ils répondent à un besoin précis.

## 5. Conditions : v-if, v-else-if, v-else et v-show

Une interface ne doit pas afficher les mêmes éléments dans toutes les situations. Un plat peut être disponible ou en rupture ; un panier peut être vide ou rempli.

- `v-if` crée ou retire le bloc du DOM selon la condition.
- `v-else-if` ajoute une autre condition à la chaîne.
- `v-else` représente le cas restant.
- `v-show` conserve l'élément dans le DOM et change sa visibilité CSS.

Choisis `v-if` lorsque l'élément doit réellement exister uniquement dans certains cas. Choisis `v-show` lorsque l'élément est fréquemment masqué puis réaffiché et qu'il est utile de le conserver. Ils ne sont donc pas interchangeables.

Un bloc `v-else` doit être placé directement après le bloc conditionnel auquel il correspond, sans élément intermédiaire qui rompe la chaîne.

## 6. Répéter une collection avec v-for

`v-for` répète un élément pour chaque entrée d'une collection. Pour un catalogue, chaque objet représente un plat. Les données peuvent contenir un identifiant, un nom, un prix et un stock.

La directive a besoin d'une clé stable, par exemple l'identifiant du plat. La clé aide Vue à associer chaque élément rendu à son identité quand la liste change.

Pourquoi éviter l'index comme clé pour une liste modifiable ? Si tu supprimes le premier plat, l'ancien deuxième élément devient le premier. Avec l'index, Vue peut réutiliser un élément rendu pour une identité différente. Cela peut produire des comportements surprenants lorsque les éléments possèdent un état interne ou des champs de formulaire.

Évite aussi les clés aléatoires créées à chaque rendu : une clé doit rester stable. Enfin, prévois un message explicite si la liste est vide ou si aucun élément ne correspond à la recherche.

## 7. Champs de formulaire avec v-model

`v-model` relie la valeur d'un champ de formulaire à une donnée Vue. Pour un champ texte, il affiche la donnée et met à jour cette donnée lorsque l'utilisateur saisit du texte.

Le modèle ne valide pas automatiquement la règle métier. Un champ peut être relié à une donnée tout en contenant une valeur incorrecte. La validation est une responsabilité distincte : vérifier, expliquer l'erreur et empêcher une action invalide.

Pour un formulaire de commande, identifie :
1. la donnée associée à chaque champ ;
2. les valeurs autorisées ;
3. le moment où la validation est effectuée ;
4. la manière d'afficher les erreurs ;
5. le comportement lorsque l'envoi réussit ou échoue.

Le frontend améliore l'expérience, mais le backend doit également vérifier les données importantes.

## 8. Erreurs fréquentes et diagnostic

- Une variable s'affiche comme du texte inattendu : vérifie si tu as oublié `:` devant un attribut dynamique.
- Une image ne se charge pas : vérifie la valeur réelle de `src`, le chemin et l'existence du fichier.
- Un clic ne fait rien : vérifie que l'événement écoute le bon élément et que la fonction existe.
- Un bloc `v-else` ne se comporte pas comme prévu : vérifie qu'il suit immédiatement le bloc conditionnel.
- Une liste se met à jour de façon étrange : vérifie la stabilité et l'unicité des clés.
- Une liste vide laisse un espace ou un écran vide : prévois un état vide.
- Un formulaire recharge la page : vérifie si le comportement natif de soumission doit être empêché avec `.prevent`.
- Le bouton accepte une action interdite : l'affichage désactivé ne remplace pas la validation de l'action elle-même.

Pour diagnostiquer, compare le résultat attendu et le résultat réel, lis la console, vérifie les données utilisées par le template et ne change qu'une chose à la fois.

## Laboratoire — Catalogue de restaurant

Construis toi-même un catalogue avec des plats comprenant identifiant, nom, prix, photo et quantité disponible.

Étapes :
1. Affiche le nom et le prix de chaque plat.
2. Affiche sa photo en utilisant une donnée pour le chemin de l'image.
3. Affiche un lien dont la destination est fournie par une donnée.
4. Affiche « Rupture » si la quantité est nulle.
5. Répète les plats avec une clé stable.
6. Ajoute un bouton qui déclenche une action.
7. Ajoute un champ de recherche et un message lorsqu'aucun résultat ne correspond.
8. Ajoute un bouton qui montre ou masque les détails.
9. Empêche les actions incompatibles avec le stock.
10. Teste la liste vide, un plat sans stock et un chemin d'image incorrect.

Ne passe pas directement au CSS. Fais fonctionner le comportement, puis améliore la présentation.

## Questions de compréhension

Avant de consulter la correction ou de passer au module suivant, explique à voix haute :
1. Quelle est la différence entre interpolation et liaison d'attribut ?
2. Pourquoi `src="imagePlat"` et `:src="imagePlat"` n'ont-ils pas le même sens ?
3. Quelle est la relation entre `v-bind:href` et `:href` ?
4. Quelle différence de fonctionnement existe entre `v-if` et `v-show` ?
5. Pourquoi une clé stable est-elle importante dans `v-for` ?
6. Quel rôle joue `v-model`, et pourquoi ne remplace-t-il pas la validation ?
7. Comment distinguer une erreur de liaison Vue d'un chemin de fichier incorrect ?

## Critères de réussite

Le laboratoire est réussi si le catalogue fonctionne avec une liste remplie, une liste vide, un plat en rupture, une recherche sans résultat et des attributs dynamiques. Tu dois pouvoir expliquer le rôle de chaque directive utilisée sans lire ce document.
