# Cours complet Vue 3 — comprendre, pratiquer et devenir autonome

> Ce document est le cours principal. Il explique les notions, leur utilité, leur fonctionnement, les différences importantes et les erreurs à reconnaître. Les laboratoires séparés servent ensuite à pratiquer sans recopier une solution.

## Comment étudier

Pour chaque chapitre : lis l'explication, prédis le résultat des exemples, essaie de les reproduire de mémoire, modifie une donnée et explique ce qui change. Ne coche une notion comme acquise que si tu sais la définir, expliquer son utilité, l'utiliser et diagnostiquer une erreur courante.

Le fil rouge est un restaurant : catalogue de plats, stock, recherche, panier, commandes, puis application connectée à une API et à Laravel.

# Partie I — Le web avant Vue

## 1. Navigateur, frontend, backend et HTTP

Le navigateur est le programme qui affiche une page et exécute le JavaScript côté utilisateur. Le frontend est l'interface et son comportement. Le backend exécute la logique côté serveur, applique les règles métier, vérifie les droits et accède généralement à une base de données.

HTML décrit la structure, CSS la présentation et JavaScript le comportement. Vue est un framework JavaScript qui aide à organiser des interfaces réactives. Il ne remplace aucune de ces technologies.

Quand une page demande des produits à un serveur, le navigateur envoie une requête HTTP. Le serveur répond avec un statut et souvent des données JSON. JSON est un format texte de données : objets, tableaux, chaînes, nombres, booléens et null. JSON n'est pas une base de données et ne contient pas de fonctions.

Exemple de cycle :
1. Le client ouvre la page.
2. Vue affiche l'interface.
3. Le frontend demande les produits à l'API.
4. Le serveur vérifie la demande et lit les données.
5. Le serveur répond en JSON.
6. Le frontend transforme la réponse en interface.

Ne confonds pas une donnée affichée par le frontend avec une donnée sécurisée. Le navigateur est contrôlé par l'utilisateur. Le backend doit revérifier les prix, les stocks, les permissions et toute règle importante avant d'enregistrer une commande.

## 2. HTML et attributs

Une balise décrit un élément, par exemple un titre, une image ou un bouton. Un attribut apporte une information à l'élément. Dans `<a href="https://example.com">Visiter</a>`, `a` est l'élément lien, `href` est son attribut et l'URL est sa valeur.

Quelques attributs :
- `src` : source d'une image ou d'un média ;
- `href` : destination d'un lien ;
- `alt` : description textuelle d'une image informative ;
- `id` : identifiant unique dans le document ;
- `class` : classe utilisable par CSS ;
- `type` : type d'un champ ou d'un bouton.

Utilise des éléments sémantiques adaptés : `header`, `nav`, `main`, `section`, `article`, `button`, `form` et des titres hiérarchisés. Un bouton sert à effectuer une action ; un lien sert à naviguer. Cette distinction améliore l'accessibilité et le comportement au clavier.

## 3. CSS, cascade et mise en page

CSS associe des règles de présentation aux éléments. Un sélecteur choisit les éléments, une propriété définit ce qui change et une valeur précise le résultat. Exemple conceptuel : la propriété `color` définit la couleur du texte.

La cascade détermine quelles règles s'appliquent lorsqu'elles se contredisent. La spécificité, l'ordre des règles et l'origine comptent. Évite de résoudre chaque conflit en ajoutant toujours plus de sélecteurs compliqués : clarifie plutôt les responsabilités des styles.

Le modèle de boîte comprend contenu, padding, bordure et marge. `box-sizing: border-box` rend généralement les dimensions plus faciles à raisonner, car la largeur inclut padding et bordure.

Flexbox sert surtout à organiser des éléments dans une dimension ; Grid sert à organiser des lignes et colonnes. Les media queries adaptent la présentation à la largeur de l'écran. Un site responsive doit rester lisible et utilisable sur téléphone, tablette et ordinateur.

## 4. JavaScript : les bases indispensables

### Variables et valeurs
`const` déclare une liaison qui ne peut pas être réassignée ; `let` permet la réassignation. Évite `var` dans le code moderne, car sa portée et son comportement peuvent surprendre. Une constante contenant un objet peut toujours avoir ses propriétés modifiées : `const` ne rend pas automatiquement l'objet immuable.

Les types courants sont string, number, boolean, undefined, null, object et les fonctions. `typeof` permet d'inspecter certaines valeurs, mais attention : `typeof null` renvoie historiquement `"object"`.

### Conditions
Une condition choisit un chemin selon une expression vraie ou fausse. `===` compare sans conversion implicite de type ; privilégie-le à `==`. Une valeur truthy est considérée vraie dans un contexte booléen ; une valeur falsy comprend notamment `false`, `0`, `""`, `null`, `undefined` et `NaN`.

### Fonctions
Une fonction regroupe un comportement réutilisable. Elle peut recevoir des paramètres et renvoyer un résultat avec `return`. Un paramètre est le nom utilisé dans la définition ; un argument est la valeur transmise lors de l'appel. Une fonction qui calcule une valeur devrait généralement éviter de modifier des données extérieures sans que cela soit attendu.

### Tableaux et objets
Un objet décrit une entité avec des propriétés, par exemple un plat avec `id`, `nom`, `prix` et `stock`. Un tableau ordonne plusieurs valeurs. Un tableau de plats est donc un tableau d'objets.

Méthodes utiles :
- `map` transforme chaque élément et retourne un nouveau tableau ;
- `filter` conserve les éléments qui satisfont une condition ;
- `find` retourne le premier élément correspondant ou `undefined` ;
- `some` vérifie si au moins un élément correspond ;
- `every` vérifie si tous les éléments correspondent ;
- `reduce` accumule les éléments en un résultat ;
- `includes` vérifie si une valeur est présente.

Ces méthodes ne sont pas interchangeables. Pour rechercher des plats par nom, pense à `filter`. Pour afficher une version transformée de chaque plat, pense à `map`. Pour trouver un plat par identifiant, pense à `find`.

### Référence et copie
Les nombres et chaînes sont des valeurs primitives. Les objets et tableaux sont manipulés par référence. Deux variables peuvent donc référencer le même objet : modifier cet objet via l'une est visible via l'autre. L'opérateur de copie superficielle `...` copie le premier niveau, mais les objets imbriqués restent partagés. Il faut comprendre cette différence avant de modifier des objets dans un tableau.

### Modules
`export` rend une valeur accessible depuis un autre fichier ; `import` la récupère. Les modules séparent le code par responsabilité. Un service API ne devrait pas être mélangé sans raison à la présentation d'une carte de plat.

### Asynchronisme
Une promesse représente le résultat futur d'une opération. `async` permet à une fonction de retourner une promesse ; `await` attend son résultat dans une fonction asynchrone. Une requête réseau peut échouer, prendre du temps ou renvoyer une erreur HTTP. Il faut prévoir les états de chargement, succès, liste vide et erreur.

## 5. Git et le travail propre

Git conserve l'historique des modifications. `git status` indique l'état du répertoire ; `git diff` montre les changements ; `git add` sélectionne ce qui entrera dans le prochain commit ; `git commit` enregistre un ensemble cohérent de changements. Une branche permet d'isoler un travail. Un merge intègre une branche dans une autre.

Avant de committer, vérifie le diff. Un commit doit représenter une intention compréhensible. Ne versionne pas les secrets, fichiers `.env`, dépendances installées ou artefacts générés inutilement. Ne remplace jamais du travail existant sans l'avoir inspecté.

# Partie II — Démarrer un projet Vue

## 6. Vue, Vite et les fichiers

Vue 3 est le framework d'interface. Vite est l'outil de développement et de compilation. Node.js permet d'exécuter des outils JavaScript sur ta machine ; npm installe les dépendances et lance les scripts déclarés dans `package.json`.

Commandes de départ :
```bash
node --version
npm --version
npm create vue@latest
cd nom-du-projet
npm install
npm run dev
```

Le programme affiche une adresse locale. Ouvre-la dans le navigateur. Pour produire les fichiers destinés à la publication, utilise `npm run build`. Le serveur de développement n'est pas le serveur de production.

Fichiers usuels :
- `package.json` : scripts et dépendances ;
- `index.html` : document HTML de départ ;
- `src/main.js` : point d'entrée qui crée et monte l'application ;
- `src/App.vue` : composant racine ;
- `src/components/` : composants réutilisables ;
- `public/` : ressources servies telles quelles ;
- `node_modules/` : dépendances installées, ne pas éditer à la main ;
- `dist/` : sortie générée par le build.

## 7. Un fichier .vue

Un composant Vue SFC (Single-File Component) rassemble généralement trois blocs :
- `<template>` : structure de l'interface ;
- `<script setup>` : logique JavaScript ;
- `<style>` : présentation CSS.

Le `template` n'est pas un fichier HTML indépendant : Vue le compile et y interprète ses directives. Avec `<script setup>`, les variables et fonctions déclarées au niveau supérieur sont disponibles dans le template. Les trois blocs restent des responsabilités distinctes, même s'ils sont réunis dans le même fichier.

## 8. Le modèle mental de Vue

Une interface est le reflet des données de l'application. Tu décris ce que l'interface doit afficher selon les données et l'état courant. Vue suit les dépendances réactives et met à jour les parties concernées lorsque ces données changent.

La réactivité ne signifie pas que chaque variable JavaScript est suivie automatiquement. Les données doivent être rendues réactives par les mécanismes Vue appropriés. Une règle métier — par exemple interdire une quantité négative — doit toujours être écrite par le développeur.

# Partie III — Templates et directives

## 9. Interpolation : afficher du texte

Les doubles accolades `{{ expression }}` affichent le résultat d'une expression JavaScript dans le texte du template. Une expression produit une valeur ; une instruction de contrôle comme `if` n'est pas une expression utilisable directement de la même manière.

Exemple :
```vue
<template>
  <h1>Menu du jour</h1>
  <p>Plat : {{ nomPlat }}</p>
  <p>Prix : {{ prix }} FCFA</p>
</template>

<script setup>
const nomPlat = 'Mafé'
const prix = 2500
</script>
```

Ici, Vue affiche les valeurs de `nomPlat` et `prix`. Si une valeur réactive change, l'affichage dépendant de cette valeur est actualisé. Garde les expressions du template simples ; les calculs métier compliqués devraient être nommés et organisés dans le script, souvent avec `computed`.

L'interpolation affiche du texte. Pour remplir un attribut HTML, il faut utiliser une liaison d'attribut.

## 10. v-bind et le raccourci :

Dans HTML, `src="photo.jpg"` donne directement à l'attribut la chaîne `photo.jpg`. Dans Vue, `:src="imagePlat"` signifie que Vue évalue l'expression JavaScript `imagePlat`, puis utilise sa valeur comme attribut `src`.

`v-bind:src="imagePlat"` et `:src="imagePlat"` sont équivalents. Le deux-points est un raccourci de `v-bind:`.

La différence se trouve dans les guillemets :
- `src="imagePlat"` : la valeur littérale est le texte `imagePlat` ;
- `:src="imagePlat"` : la valeur est le contenu de la variable `imagePlat`.

On utilise `:href` pour une destination de lien dynamique, `:alt` pour un texte alternatif dynamique, `:class` pour une classe conditionnelle, et `:disabled` pour l'état désactivé d'un bouton. On n'ajoute pas `:` à chaque attribut : on l'utilise lorsqu'une valeur doit être évaluée comme une expression Vue.

## 11. v-on et les événements

`v-on:click` écoute un clic ; son raccourci est `@click`. Un événement représente quelque chose qui arrive, comme un clic, une saisie ou l'envoi d'un formulaire. Le gestionnaire est la fonction appelée en réponse.

Un événement utilisateur exprime une intention. Dans une architecture claire, le bouton déclenche une action explicite plutôt que de modifier arbitrairement plusieurs morceaux d'interface. Les modificateurs, comme `.prevent`, indiquent à Vue de gérer certains comportements natifs. `@submit.prevent` empêche le rechargement classique du formulaire lorsque le formulaire est géré côté Vue.

## 12. v-if, v-else-if, v-else et v-show

`v-if` ajoute ou retire un bloc du DOM selon une condition. `v-else-if` et `v-else` forment une chaîne conditionnelle adjacente. `v-show` conserve l'élément dans le DOM et modifie sa visibilité CSS.

Choix :
- `v-if` si l'existence du bloc dépend réellement de la condition ;
- `v-show` si le bloc doit être fréquemment masqué et affiché.

Ce n'est pas seulement une différence d'écriture : `v-if` implique création/destruction du bloc, alors que `v-show` conserve son élément. Un `v-else` doit suivre directement un bloc `v-if` ou `v-else-if` compatible.

## 13. v-for et :key

`v-for` répète une portion du template pour chaque élément d'une liste. La directive doit recevoir une collection et une clé stable, habituellement un identifiant unique tel que `plat.id`.

La clé aide Vue à retrouver l'identité de chaque élément lorsque la liste change. Si une liste peut être filtrée, triée ou supprimée, l'index comme clé peut faire correspondre un ancien état à un mauvais élément. Ne génère pas une clé aléatoire à chaque rendu : elle doit rester stable.

Affiche aussi les états de liste vide. Une interface ne doit pas simplement disparaître si aucun plat ne correspond à la recherche.

## 14. v-model et les formulaires

`v-model` synchronise un champ de formulaire avec une donnée Vue. Pour un champ texte, il met à jour la donnée lorsque l'utilisateur saisit et affiche la donnée dans le champ. Pour une case à cocher ou un groupe de choix, le type de valeur dépend du contrôle.

Il s'agit d'un raccourci Vue qui coordonne la valeur et l'événement du champ ; ce n'est pas une magie HTML. Pour comprendre un formulaire, identifie la donnée qui représente la saisie, les règles de validation, le moment de validation et le résultat en cas d'erreur.

La validation frontend améliore l'expérience, mais le backend doit refaire les vérifications importantes. Ne considère jamais une valeur comme fiable simplement parce qu'un champ HTML la limite.

# Partie IV — Réactivité et logique

## 15. ref et .value

`ref(valeur)` crée un objet référence réactif qui contient la valeur dans sa propriété `.value`. Dans le script JavaScript, on lit ou modifie généralement `.value`. Dans le template, une ref de premier niveau est généralement déballée automatiquement : on écrit son nom sans `.value`.

Pourquoi cette différence ? Le script manipule un objet JavaScript ; Vue fournit au template un mécanisme de déballage pour rendre l'affichage plus simple. Ne généralise pas ce déballage à toutes les expressions imbriquées : le comportement dépend du contexte.

`ref` convient aux valeurs primitives comme un nombre, une chaîne ou un booléen, et fonctionne aussi pour des objets. Il est souvent un choix simple et polyvalent.

## 16. reactive et ses limites

`reactive(objet)` retourne un proxy qui permet à Vue de suivre les lectures et modifications des propriétés de cet objet. Dans le script, on accède directement aux propriétés du proxy, sans `.value`.

Il faut conserver la relation avec le proxy. Si tu extrais une propriété primitive dans une variable séparée, cette variable n'est pas automatiquement une liaison réactive à la propriété originale. De même, remplacer la variable qui contient le proxy par un nouvel objet peut faire perdre la relation attendue. Quand une valeur doit être remplacée facilement, `ref` est souvent plus simple.

Choix pratique : utilise `ref` comme choix par défaut lorsque tu veux une référence réactive claire ; utilise `reactive` lorsque travailler directement avec les propriétés d'un objet rend le code plus lisible. La cohérence compte plus qu'une règle absolue.

## 17. computed : les valeurs dérivées

Une valeur dérivée est calculée à partir d'autres données. Le nombre d'articles du panier ou le prix total ne devraient pas être maintenus manuellement en parallèle si on peut les calculer à partir des lignes du panier.

`computed` déclare une valeur calculée qui dépend de données réactives. Vue met le résultat en cache et le recalcule lorsque ses dépendances changent. Elle est normalement en lecture seule et sans effet secondaire.

Une méthode peut calculer le même résultat, mais elle est appelée chaque fois qu'on l'invoque. Une propriété `computed` met son résultat en cache selon ses dépendances. Utilise `computed` pour une valeur dérivée ; utilise une fonction/méthode pour une action ou un calcul qu'on veut exécuter à un moment précis.

## 18. watch et watchEffect

Un watcher sert à déclencher un effet secondaire lorsqu'une donnée change : enregistrer une préférence, démarrer une requête, synchroniser une ressource ou réagir à un changement externe. Un effet secondaire est une action qui dépasse le simple calcul d'une valeur : écriture de stockage, requête réseau, journalisation ou modification d'un système externe.

`watch(source, callback)` observe une source explicite. Il permet de distinguer la valeur précédente et la nouvelle valeur. `watchEffect(callback)` exécute le callback et détecte automatiquement les dépendances réactives lues pendant son exécution synchrone.

N'utilise pas `watch` simplement pour calculer le total d'un panier : c'est le rôle de `computed`. Pour les requêtes déclenchées par une recherche, pense aussi aux réponses arrivant dans le désordre et au nettoyage/à l'annulation de l'opération précédente.

## 19. Classes, styles et états d'interface

Vue permet de lier `:class` et `:style` à des données. Utilise ces liaisons pour refléter un état réel : bouton désactivé, plat indisponible, élément sélectionné ou erreur. Évite de manipuler manuellement les classes du DOM lorsque l'état peut être décrit dans les données.

Une interface complète prévoit au minimum les états normal, vide, chargement, erreur et succès lorsque ces états sont possibles. Le style ne remplace pas un message compréhensible : une erreur ne doit pas être signalée uniquement par la couleur.

# Partie V — Composants et architecture

## 20. Pourquoi découper en composants ?

Un composant doit avoir une responsabilité identifiable. Une carte de plat affiche un plat et expose les actions pertinentes ; une liste de plats organise les cartes ; un panier calcule/présente la sélection ; une page orchestre les grandes parties de l'écran.

Ne crée pas un composant pour chaque ligne par réflexe, et ne garde pas non plus toute l'application dans un fichier géant. Découpe lorsqu'une partie a une responsabilité claire, est réutilisée, a une logique distincte ou mérite d'être testée séparément.

## 21. Props : parent vers enfant

Une prop est une donnée fournie par un composant parent à un composant enfant. Elle décrit le contrat d'entrée de l'enfant : de quelles données a-t-il besoin pour fonctionner ?

L'enfant ne doit pas modifier directement une prop. Le parent est propriétaire de la donnée et doit rester responsable de son changement. Si l'enfant veut signaler une action, il émet un événement au parent.

Cette règle rend le flux des données compréhensible : données vers le bas, intentions vers le haut. Les objets imbriqués demandent de l'attention, car une référence d'objet peut permettre des mutations indirectes ; évite de contourner la responsabilité du parent.

## 22. Emits : enfant vers parent

Un événement personnalisé permet à un enfant d'annoncer une intention, par exemple « ajouter ce plat au panier » ou « supprimer cette ligne ». L'enfant ne décide pas nécessairement de la manière dont le parent exécutera l'action.

Déclare les événements attendus avec `defineEmits`. Les noms doivent exprimer clairement l'intention. Les données passées avec l'événement doivent être limitées à ce dont le parent a besoin. Un événement n'est pas une variable partagée : c'est un mécanisme de communication.

## 23. Slots

Un slot permet au parent de fournir du contenu à l'intérieur d'un composant enfant. Le composant définit une structure réutilisable et le parent injecte le contenu approprié. Le slot par défaut convient au contenu principal ; les slots nommés permettent de distinguer plusieurs zones, comme un en-tête et un pied de carte.

Choisis les props lorsque le composant reçoit des données structurées ; choisis les slots lorsque le parent doit personnaliser le contenu rendu dans une zone.

## 24. v-model sur un composant

Sur un composant personnalisé, `v-model` s'appuie sur une prop et un événement de mise à jour convenus. Le parent reste propriétaire de la donnée, et l'enfant propose une nouvelle valeur. Ce mécanisme rend les composants de formulaire réutilisables sans cacher qui possède l'état.

## 25. Cycle de vie et template refs

Un composant passe par des phases : création/préparation, montage dans le DOM, mises à jour et démontage. Les hooks tels que `onMounted` et `onUnmounted` permettent de démarrer puis nettoyer des opérations qui dépendent du DOM ou de ressources externes.

Une template ref permet de référencer un élément DOM ou une instance de composant. Utilise-la lorsque tu as réellement besoin d'interagir avec le DOM, par exemple pour placer le focus. Privilégie l'état déclaratif de Vue pour les changements d'interface ordinaires plutôt que de manipuler le DOM manuellement.

## 26. Composables et structure de dossiers

Un composable est une fonction réutilisable qui encapsule une logique liée à la réactivité Vue. Par convention, son nom commence souvent par `use`, comme `useCart` ou `useProducts`. Il partage de la logique, pas nécessairement un état global unique : chaque appel peut avoir son propre état selon sa conception.

Organisation possible :
- `components/` : éléments réutilisables d'interface ;
- `views/` ou `pages/` : écrans associés aux routes ;
- `composables/` : logique réactive réutilisable ;
- `services/` : communication API et services externes ;
- `router/` : configuration des routes ;
- `stores/` : état partagé Pinia ;
- `types/` : types TypeScript.

Ce sont des conventions, pas des dossiers obligatoires. Choisis une structure proportionnée à la taille de l'application et évite les couches qui ne font que transmettre les appels sans responsabilité.

# Partie VI — Formulaires, données et API

## 27. CRUD et validation

CRUD signifie Create, Read, Update, Delete : créer, lire, modifier et supprimer. Pour chaque opération, définis la donnée source, l'action, les règles, le résultat attendu et le comportement en cas d'erreur.

Une validation utile explique ce qui est incorrect et comment le corriger. Vérifie les champs obligatoires, les types, les valeurs positives, les limites métier et les dépendances entre champs. Garde les données saisies si une validation échoue. Associe les erreurs aux champs et rends-les accessibles aux lecteurs d'écran.

## 28. localStorage et JSON

`localStorage` conserve des chaînes dans le navigateur après fermeture de la page. Il peut servir à enregistrer une préférence ou un panier de démonstration. Pour stocker un objet, convertis-le en JSON ; pour le relire, analyse le JSON et gère les valeurs absentes ou corrompues.

Le stockage navigateur n'est pas une base centrale, n'est pas synchronisé automatiquement entre appareils et peut être effacé par l'utilisateur. Ne stocke pas de mots de passe, secrets ou données sensibles. Pour une vraie commande, le serveur reste la source d'autorité.

## 29. fetch, HTTP et API

`fetch` effectue une requête HTTP et retourne une promesse de réponse. Un point important : une réponse HTTP comme 404 ou 500 ne fait généralement pas rejeter la promesse ; il faut vérifier `response.ok` ou le statut. Les erreurs réseau, elles, peuvent rejeter la promesse.

Une requête API doit gérer :
- chargement ;
- succès avec données ;
- succès sans résultat ;
- erreur HTTP ;
- erreur réseau ;
- annulation ou remplacement de requête si nécessaire.

Vérifie le format des données reçues : le frontend ne doit pas supposer aveuglément que la réponse est toujours correcte. Garde la logique HTTP dans un service quand cela améliore la séparation des responsabilités.

## 30. Recherche, filtre, tri et pagination

Le filtrage choisit les éléments qui correspondent à un critère. Le tri change leur ordre. La pagination divise une collection en pages. Sur une petite liste déjà chargée, ces opérations peuvent se faire côté client. Sur un gros volume ou des données qui changent souvent, le serveur doit généralement participer.

Ne modifie pas accidentellement la liste source lorsqu'un affichage filtré est calculé. Une propriété calculée peut produire la liste visible à partir de la source et des critères. Traite les recherches sans résultat et les valeurs de recherche vides.

# Partie VII — Navigation et état partagé

## 31. Vue Router

Vue Router associe une URL à un composant de page. `RouterLink` crée des liens de navigation adaptés à une application Vue et `RouterView` indique où afficher la page courante. Une route dynamique peut représenter le détail d'un plat à partir de son identifiant ; une query string peut représenter un filtre ou une recherche.

Une page 404 doit traiter les chemins inconnus. Les routes imbriquées permettent de partager un layout. La navigation doit être testée avec les liens, le bouton retour et le rechargement d'une URL profonde.

## 32. Guards et sécurité

Un guard peut empêcher une navigation ou la rediriger selon l'état de l'application. Il améliore l'expérience, mais **un guard frontend n'est pas une protection de sécurité suffisante**. Un utilisateur peut appeler directement l'API sans passer par l'interface. Le backend doit vérifier l'authentification et les autorisations à chaque opération protégée.

## 33. Pinia et stratégie d'état

Pinia est la bibliothèque officielle de gestion d'état largement utilisée dans l'écosystème Vue. Un store peut réunir un état partagé, des getters calculés et des actions.

N'envoie pas toutes les données dans un store par défaut. Choisis selon leur responsabilité :
- état local : utilisé par un seul composant ou une petite zone ;
- état dans l'URL : recherche, filtre, page ou élément consulté que l'on veut partager par lien ;
- état serveur : données dont le backend est la source d'autorité ;
- état global : panier ou session d'interface partagé entre plusieurs pages, selon les besoins.

Un store frontend ne remplace pas une base de données. La persistance et les règles métier critiques doivent être gérées au bon endroit.

# Partie VIII — TypeScript, tests et qualité

## 34. TypeScript avec Vue

TypeScript ajoute une vérification statique des types à JavaScript. Il aide à détecter certains problèmes avant l'exécution et à documenter les contrats. Les types et interfaces décrivent la forme attendue d'une donnée ; les unions représentent plusieurs possibilités contrôlées ; les génériques rendent une fonction ou un type réutilisable pour différentes formes de données.

TypeScript ne valide pas automatiquement les données reçues du réseau au moment de l'exécution. Une réponse API doit être considérée comme externe tant qu'elle n'a pas été vérifiée. Commence par des types simples, puis typage des props, événements, fonctions et réponses.

## 35. Tests

Un test vérifie un comportement attendu. Un test unitaire cible une fonction ou une petite unité ; un test de composant vérifie rendu et interactions ; un test de bout en bout simule un parcours réel dans le navigateur.

Teste d'abord le comportement utile : calcul du panier, validation, liste vide, erreurs API, événements, navigation et permissions côté serveur. Un test doit être compréhensible et indépendant autant que possible. Un build réussi ne prouve pas que les comportements sont corrects ; un test vert ne prouve pas non plus que toutes les situations sont couvertes.

Outils fréquents :
- Vitest pour les tests unitaires ;
- Vue Test Utils pour monter et interagir avec des composants ;
- Playwright pour les parcours navigateur ;
- ESLint et formatage pour les conventions et erreurs détectables statiquement.

## 36. Accessibilité

Une interface accessible peut être utilisée au clavier et avec des technologies d'assistance. Associe les champs à des labels, conserve un ordre de titres cohérent, utilise des boutons et liens sémantiques, rends les erreurs compréhensibles et visibles, assure un contraste suffisant et déplace le focus de façon prévisible dans les dialogues.

N'utilise pas la couleur comme seul moyen d'indiquer un état. Les images informatives ont un texte alternatif pertinent ; les images décoratives peuvent avoir un texte alternatif vide. Teste au clavier, pas uniquement à la souris.

## 37. Sécurité et performance

N'injecte pas de HTML non fiable. Ne considère pas les validations frontend comme une protection. N'expose pas de secret dans le code envoyé au navigateur. Le backend doit appliquer les règles d'accès et valider les entrées.

Pour les performances : évite les calculs inutiles, garde les composants cohérents, charge les grosses pages à la demande lorsque cela se justifie, optimise les images et mesure avant d'optimiser. La meilleure optimisation n'est pas d'ajouter des outils au hasard, mais d'identifier le vrai coût.

# Partie IX — Nuxt, PWA et Laravel

## 38. Nuxt, SSR, SSG et hydratation

Nuxt est un framework construit autour de Vue qui apporte notamment routage basé sur les fichiers et plusieurs stratégies de rendu. En rendu côté serveur (SSR), le serveur produit le HTML de la page pour la requête. En génération statique (SSG), les pages sont générées à l'avance. L'hydratation est le processus par lequel Vue attache le comportement JavaScript à un HTML déjà rendu.

Ces stratégies ont des compromis : SEO, temps d'affichage, coût serveur, données personnalisées et complexité. Elles ne sont pas nécessaires à toutes les applications. Apprends d'abord Vue côté client, puis introduis Nuxt lorsque le besoin le justifie.

## 39. PWA

Une Progressive Web App peut offrir une expérience installable et des fonctionnalités hors ligne selon sa configuration. Un service worker peut intercepter certaines requêtes et gérer le cache. Il faut prévoir la mise à jour du cache, les ressources obsolètes, les permissions et les limites du mode hors ligne.

Ne promets pas une commande comme envoyée si elle n'a pas été confirmée par le serveur. Une action hors ligne doit afficher clairement son statut et synchroniser de façon fiable lorsque le réseau revient.

## 40. Intégrer Vue et Laravel

Vue peut servir l'interface tandis que Laravel expose une API. Laravel reste responsable de l'authentification, des autorisations, de la validation métier, des transactions et de la persistance. Vue gère la présentation, les interactions et les états d'interface.

Définis un contrat API clair : URL, méthode HTTP, format de requête, format de réponse, erreurs et codes de statut. Gère la session ou les jetons selon l'architecture choisie, la configuration CORS et la protection CSRF si elle s'applique. Ne mets jamais une clé privée dans le frontend.

Lorsqu'un client commande deux pots à 200 FCFA, le frontend peut afficher un aperçu, mais Laravel doit recalculer le prix et vérifier la disponibilité. Le prix envoyé par le client n'est jamais une preuve fiable. L'état de commande affiché doit refléter une réponse serveur confirmée.

## 41. Déploiement

Le build génère les fichiers de production. Les variables nécessaires au frontend sont intégrées au bundle et ne doivent donc pas contenir de secrets. Configure les URL API et les environnements selon les conventions de l'outil. Teste l'application construite, les routes profondes, les erreurs réseau et les ressources statiques.

Un déploiement fiable implique une version contrôlée, une compilation réussie, des tests pertinents, une configuration correcte et la possibilité de diagnostiquer les erreurs en production.

# Partie X — Méthode de résolution de problèmes

## 42. Diagnostiquer sans deviner

Quand quelque chose ne fonctionne pas :
1. Décris le résultat attendu et le résultat réel.
2. Reproduis le problème avec le plus petit scénario possible.
3. Lis le premier message d'erreur pertinent dans la console ou le terminal.
4. Localise le fichier et la ligne concernés.
5. Formule une hypothèse précise.
6. Change une seule chose.
7. Reproduis le test.
8. Vérifie que tu n'as pas cassé un autre comportement.
9. Explique la cause et le correctif avec tes mots.

Ne corrige pas une erreur de données avec du CSS. Ne corrige pas un problème d'import en réécrivant toute l'application. Une erreur de compilation, une erreur JavaScript, une réponse HTTP en échec et un problème de style sont des catégories différentes.

## 43. Questions de conception à poser avant de coder

Pour chaque fonctionnalité, note :
- Quel problème utilisateur résout-elle ?
- Quelles données sont nécessaires et qui en est propriétaire ?
- Quelles actions peuvent modifier ces données ?
- Quelles règles doivent toujours être respectées ?
- Quelles situations limites existent ?
- Que se passe-t-il pendant le chargement ou en cas d'échec ?
- Quel composant est responsable de l'affichage ?
- Quelle partie mérite un composable, un service ou un store ?
- Comment vérifier le comportement ?
- Comment expliquer ce choix à un autre développeur ?

# Évaluation finale

Construis progressivement une application de restaurant qui comporte :
1. Catalogue de plats avec nom, prix, photo et disponibilité.
2. Recherche, filtres et tri.
3. Gestion de stock avec règles empêchant les valeurs invalides.
4. Panier avec quantités, sous-totaux et total calculés.
5. Formulaire de commande accessible et validé.
6. Plusieurs composants avec props, emits et slots pertinents.
7. Navigation multi-pages et page 404.
8. Persistance adaptée aux données qui peuvent rester dans le navigateur.
9. Chargement d'une API avec états loading, error, empty et success.
10. Tests des calculs, des interactions et du parcours de commande.
11. Types explicites si le projet utilise TypeScript.
12. Intégration avec une API Laravel et gestion claire des erreurs.
13. Interface responsive et utilisable au clavier.
14. Build de production, déploiement et instructions de reprise.

## Critères de maîtrise

Tu es prêt à passer à l'étape suivante quand tu peux :
- expliquer chaque mécanisme utilisé sans réciter une définition ;
- reconstruire une version simple sans copier le cours ;
- justifier où se trouve l'état et pourquoi ;
- expliquer les limites de ta solution ;
- reproduire et diagnostiquer une erreur ;
- tester les cas normaux et les cas limites ;
- modifier une exigence sans devoir recommencer toute l'application.

Le but n'est pas de mémoriser toutes les API. Le but est de savoir raisonner, trouver la bonne partie de la documentation, vérifier ton hypothèse et construire une solution maintenable.
