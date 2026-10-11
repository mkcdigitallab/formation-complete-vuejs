# Vue 3 — notions essentielles de l'écosystème, expliquées avec des exemples

Ce module complète les fondations. Pour chaque notion, tu dois savoir **à quel problème elle répond, quand l'utiliser, comment elle fonctionne, ce qu'elle ne fait pas et comment vérifier ton résultat**. Les exemples utilisent Vue 3 avec `<script setup>` et JavaScript.

## Préparer le terrain

On prendra une petite application de restaurant comme fil conducteur : une liste de plats, un détail de plat, un formulaire de commande et des pages Catalogue, Détail et Commandes.

Avant de choisir une API Vue, distingue :
- **état** : les données qui peuvent changer ;
- **rendu** : ce que Vue affiche à partir de cet état ;
- **effet secondaire** : une action extérieure au calcul du rendu (requête HTTP, timer, écouteur DOM, stockage) ;
- **propriété calculée** : une valeur dérivée d'autres données ;
- **navigation** : l'URL et la page actuellement affichée ;
- **état partagé** : une donnée dont plusieurs composants ont besoin.

Ne choisis pas un outil juste parce qu'il existe. Choisis-le parce que son rôle correspond au problème.

---

## 1. Lifecycle hooks — cycle de vie d'un composant

### À quoi ça sert ?

Un composant Vue traverse plusieurs étapes : Vue prépare son instance, l'insère dans le DOM, le met à jour quand ses dépendances changent, puis le démonte. Les hooks sont des points où tu peux exécuter du code lié à ces étapes.

Les hooks les plus utiles avec Composition API :

| Hook | Quand ? | Exemple de besoin |
|---|---|---|
| `onBeforeMount` | Juste avant le premier affichage dans le DOM | Rarement nécessaire au quotidien |
| `onMounted` | Après insertion du DOM du composant | Mettre le focus, démarrer un outil DOM, lancer une première opération |
| `onBeforeUpdate` | Avant une mise à jour DOM déclenchée par l'état | Lire exceptionnellement l'ancien état DOM |
| `onUpdated` | Après la mise à jour du DOM | Intégration particulière avec une bibliothèque DOM |
| `onBeforeUnmount` | Juste avant retrait du composant | Préparer l'arrêt d'une ressource |
| `onUnmounted` | Après retrait du composant | Arrêter un timer ou retirer un écouteur |

### Exemple expliqué

Un composant de recherche doit actualiser une horloge toutes les secondes pendant qu'il est affiché. Au montage, il démarre un timer ; au démontage, il l'arrête. Sans nettoyage, le timer pourrait continuer après le départ de la page et provoquer du travail inutile.

```vue
<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const maintenant = ref(new Date())
let timerId

onMounted(() => {
  timerId = window.setInterval(() => {
    maintenant.value = new Date()
  }, 1000)
})

onUnmounted(() => {
  window.clearInterval(timerId)
})
</script>

<template>
  <p>Heure actuelle : {{ maintenant.toLocaleTimeString() }}</p>
</template>
```

**Pourquoi `onMounted` ?** Le composant existe dans le DOM à ce moment. **Pourquoi `onUnmounted` ?** Il faut libérer la ressource créée. Les hooks de Composition API doivent être enregistrés synchroniquement pendant l'exécution du setup du composant, pas dans un timer ou après un `await` arbitraire.

### Pièges fréquents

- `onMounted` ne signifie pas que toutes les images, toutes les requêtes et tous les composants asynchrones de l'application ont terminé.
- Ne modifie pas l'état sans raison dans `onUpdated` : cela peut déclencher une autre mise à jour et créer une boucle.
- N'utilise pas un hook pour calculer une valeur qui dépend simplement d'autres données : utilise plutôt `computed`.
- En rendu côté serveur, le DOM n'existe pas ; les hooks dépendant du DOM ne s'exécutent pas côté serveur.

### À toi

1. Ajoute un compteur qui augmente chaque seconde.
2. Quitte la page ou masque/démonte le composant.
3. Vérifie que le timer est arrêté.
4. Explique ce qui pourrait arriver si le nettoyage était supprimé.

---

## 2. Watchers — `watch` et `watchEffect`

### Différence avec `computed`

- **`computed`** produit une valeur dérivée : par exemple le prix total du panier.
- **`watch`** observe une source déterminée et déclenche un effet quand elle change : par exemple enregistrer une préférence ou lancer une recherche HTTP.
- **`watchEffect`** exécute immédiatement une fonction et détecte automatiquement les dépendances réactives lues pendant son exécution.

### Exemple : enregistrer une préférence

```vue
<script setup>
import { ref, watch } from 'vue'

const recherche = ref('')

watch(recherche, (nouvelleValeur, ancienneValeur) => {
  console.log('Recherche modifiée :', ancienneValeur, '→', nouvelleValeur)
})
</script>

<template>
  <label>
    Rechercher un plat
    <input v-model="recherche">
  </label>
</template>
```

Ici, la source surveillée est précisément `recherche`. Le callback reçoit l'ancienne et la nouvelle valeur. Par défaut, `watch` n'exécute pas le callback immédiatement ; l'option `immediate: true` permet de le lancer dès le départ.

### Observer une propriété d'objet

Avec un objet réactif, surveiller l'objet et surveiller une de ses propriétés ne sont pas toujours la même chose. Pour suivre une propriété précise, fournis une fonction source, par exemple `() => filtres.categorie`. Le suivi profond (`deep: true`) examine aussi les changements imbriqués, mais peut coûter plus cher et ne doit pas être activé par réflexe.

### Exemple : éviter une réponse de recherche périmée

Quand l'utilisateur tape vite, plusieurs requêtes peuvent se chevaucher. La requête la plus lente peut finir après la plus récente. Utilise le mécanisme de nettoyage du watcher pour annuler la requête précédente.

```vue
<script setup>
import { ref, watch } from 'vue'

const recherche = ref('')
const resultats = ref([])
const erreur = ref('')
const chargement = ref(false)

watch(recherche, async (terme, _ancienTerme, onCleanup) => {
  const controleur = new AbortController()
  onCleanup(() => controleur.abort())

  if (!terme.trim()) {
    resultats.value = []
    erreur.value = ''
    chargement.value = false
    return
  }

  chargement.value = true
  erreur.value = ''

  try {
    const reponse = await fetch(
      `https://api.example.test/plats?q=${encodeURIComponent(terme)}`,
      { signal: controleur.signal }
    )

    if (!reponse.ok) throw new Error(`HTTP ${reponse.status}`)
    resultats.value = await reponse.json()
  } catch (cause) {
    if (cause.name !== 'AbortError') erreur.value = 'Impossible de charger les plats.'
  } finally {
    if (!controleur.signal.aborted) chargement.value = false
  }
})
</script>
```

L'adresse est illustrative : remplace-la par une API réelle ou celle de ton projet. Le nettoyage annule la requête précédente. Le test du type d'erreur évite de montrer une annulation normale comme un échec.

### À retenir

- Ne fais pas une requête HTTP dans un `computed`.
- Utilise `watch` quand tu connais la source à observer ; utilise `watchEffect` quand l'effet dépend naturellement de plusieurs valeurs lues.
- Un watcher peut retourner une fonction d'arrêt si tu dois l'arrêter explicitement.
- Attention aux boucles : un watcher qui modifie continuellement sa propre source peut se relancer sans fin.

### À toi

Observe le terme de recherche, puis observe aussi une catégorie. Écris ce qui doit arriver quand le terme est vide, quand l'API échoue et quand l'utilisateur tape rapidement.

---

## 3. Template refs — accéder à un élément du DOM

### Pourquoi en avoir besoin ?

Vue préfère un rendu déclaratif : tu modifies l'état et Vue met l'interface à jour. Une template ref est utile lorsque tu dois appeler une API impérative du navigateur, comme `focus()`, `scrollIntoView()` ou mesurer une taille.

```vue
<script setup>
import { onMounted, ref } from 'vue'

const champRecherche = ref(null)

onMounted(() => {
  champRecherche.value?.focus()
})
</script>

<template>
  <label for="recherche">Rechercher</label>
  <input id="recherche" ref="champRecherche">
</template>
```

Le nom `champRecherche` relie la variable à l'attribut `ref` du template. Avant le montage, la valeur est généralement `null`, car l'élément n'existe pas encore. Après montage, elle référence l'élément DOM.

### Cas dynamiques

Si l'élément est conditionné par `v-if`, la ref peut redevenir `null` lorsqu'il disparaît. Vérifie son existence avant de l'utiliser. Pour des listes, les refs ne sont pas automatiquement un tableau ordonné fiable dans tous les cas : si tu as besoin d'identifier les éléments, utilise une stratégie explicite.

Une ref sur un composant enfant donne accès à son instance exposée, mais un enfant écrit avec `<script setup>` n'expose pas tout automatiquement. Si le parent doit appeler une méthode publique, l'enfant peut choisir de l'exposer avec `defineExpose`. Ne transforme pas cette possibilité en moyen de contourner systématiquement props et événements.

### À toi

Crée un bouton « Ajouter un plat ». Après ajout, place le focus sur le champ du prochain plat. Teste aussi le cas où le formulaire est masqué.

---

## 4. Async components — composants chargés à la demande

### Le problème

Une grande application peut contenir des écrans lourds qui ne sont pas nécessaires dès l'ouverture. Un composant asynchrone permet de charger son code lorsque Vue en a besoin. Cela peut réduire le JavaScript initial, mais il faut vérifier le gain réel et prévoir le chargement/échec si nécessaire.

```vue
<script setup>
import { defineAsyncComponent } from 'vue'

const RapportCommandes = defineAsyncComponent({
  loader: () => import('./components/RapportCommandes.vue'),
  loadingComponent: {
    template: '<p role="status">Chargement du rapport…</p>'
  },
  errorComponent: {
    template: '<p role="alert">Le rapport ne peut pas être chargé.</p>'
  },
  delay: 200,
  timeout: 10000
})
</script>

<template>
  <RapportCommandes />
</template>
```

`import()` retourne une promesse. `defineAsyncComponent` donne à Vue un composant qu'il peut résoudre lorsque nécessaire. Dans une vraie application, les composants de chargement et d'erreur peuvent être des fichiers Vue dédiés, plus faciles à tester et à traduire.

### Ne pas confondre

- **Composant asynchrone** : le code du composant est chargé à la demande.
- **Appel API** : les données sont chargées depuis un serveur.
- **Vue Router lazy loading** : une route peut utiliser `() => import('./views/CommandesView.vue')` pour séparer le code de cette page. C'est souvent la bonne solution pour les pages entières.

### À toi

Charge à la demande une fenêtre de statistiques qui n'est pas nécessaire au premier affichage. Compare le build avant/après et vérifie le comportement si le chunk ne peut pas être téléchargé.

---

## 5. Composables — partager une logique réactive

### Définition utile

Un composable est une fonction JavaScript qui utilise les API de Composition Vue pour encapsuler et réutiliser une logique. Par convention, son nom commence par `use`, par exemple `useCounter`, `useProducts` ou `useOnlineStatus`.

Un composable ne signifie pas automatiquement « état global ». Selon sa conception, chaque appel peut créer son propre état, ou plusieurs appels peuvent partager un état intentionnellement. Il peut utiliser `ref`, `computed`, `watch` et des hooks de cycle de vie.

### Exemple : logique réutilisable de compteur

```js
// src/composables/useCounter.js
import { computed, ref } from 'vue'

export function useCounter(initialValue = 0) {
  const count = ref(initialValue)
  const double = computed(() => count.value * 2)

  function increment() {
    count.value++
  }

  function reset() {
    count.value = initialValue
  }

  return { count, double, increment, reset }
}
```

Dans un composant, tu appelles `useCounter(5)` et récupères les valeurs et fonctions. Le composable cache l'organisation de la logique, pas le comportement : le composant reste responsable de l'interface.

### Exemple métier : `useProducts`

Un composable de catalogue peut posséder `products`, `loading`, `error` et une fonction `loadProducts()`. Le composant affiche les données, tandis que le composable coordonne le chargement. Si plusieurs composants doivent partager exactement le même état de catalogue, décide explicitement si un store Pinia est plus adapté.

### Où mettre quoi ?

- `components/` : interface réutilisable.
- `composables/` : logique réactive réutilisable.
- `services/` : communication HTTP et adaptation des données externes.
- `stores/` : état partagé par plusieurs zones/pages.
- `views/` : pages associées aux routes.

Ne crée pas un composable pour une simple ligne de code qui n'a aucune logique réutilisable. Évite aussi de placer toutes les responsabilités dans un seul composable géant.

### À toi

Extrais la logique de recherche et de chargement des plats d'une page vers `useProducts`. La page ne doit plus connaître les détails de la requête HTTP.

---

## 6. Custom directives — directives personnalisées

### À quoi ça sert ?

Une directive personnalisée ajoute un comportement bas niveau à un élément du DOM. Elle est pertinente pour un comportement DOM réutilisable, comme le focus automatique. Pour la logique d'interface habituelle, préfère les composants, les événements et l'état déclaratif.

### Exemple : directive `v-focus`

```js
// src/directives/focus.js
export const vFocus = {
  mounted(element) {
    element.focus()
  }
}
```

```vue
<script setup>
import { vFocus } from '../directives/focus.js'
</script>

<template>
  <input v-focus aria-label="Nom du plat">
</template>
```

Avec `<script setup>`, une variable locale nommée `vFocus` est reconnue comme directive locale. Le hook `mounted` s'exécute quand l'élément est inséré dans le DOM. Une directive peut définir d'autres hooks comme `updated` ou `unmounted` si le comportement doit suivre les changements ou nettoyer une ressource.

### Quand ne pas en créer ?

Si le comportement concerne une grosse interface avec état, plusieurs actions et structure HTML, un composant est souvent plus clair. Une directive ne doit pas cacher des règles métier ni créer des effets DOM difficiles à prévoir.

### Accessibilité

Le focus automatique doit être utilisé avec discernement : déplacer le focus sans raison peut désorienter une personne au clavier ou utilisant un lecteur d'écran. Fournis un nom accessible aux champs et vérifie l'ordre de navigation.

### À toi

Crée une directive qui applique une infobulle simple, puis demande-toi si un composant ou l'attribut HTML natif serait plus approprié.

---

## 7. Dynamic components — choisir un composant à afficher

### Besoin

Parfois, une zone de l'écran doit afficher une vue parmi plusieurs : « Détails », « Ingrédients » ou « Avis ». Tu peux utiliser `<component :is="...">`. La valeur de `:is` peut être le nom d'un composant importé ou une chaîne adaptée.

```vue
<script setup>
import { ref } from 'vue'
import DetailsPlat from './DetailsPlat.vue'
import IngredientsPlat from './IngredientsPlat.vue'
import AvisPlat from './AvisPlat.vue'

const ongletActif = ref('details')

const onglets = {
  details: DetailsPlat,
  ingredients: IngredientsPlat,
  avis: AvisPlat
}
</script>

<template>
  <nav aria-label="Informations sur le plat">
    <button @click="ongletActif = 'details'">Détails</button>
    <button @click="ongletActif = 'ingredients'">Ingrédients</button>
    <button @click="ongletActif = 'avis'">Avis</button>
  </nav>

  <component :is="onglets[ongletActif]" />
</template>
```

La variable contient la clé de l'onglet choisi. L'objet `onglets` associe cette clé au composant. Vue affiche le composant correspondant. Dans un exemple complet, ajoute un état sélectionné accessible (`aria-current`, `aria-selected` selon le modèle choisi) et un style visible.

### Et `KeepAlive` ?

Par défaut, changer de composant peut démonter l'ancien et créer le nouveau. `<KeepAlive>` peut conserver en mémoire l'état d'un composant lorsqu'on change d'onglet. Il faut alors connaître les hooks `onActivated` et `onDeactivated`. Ne conserve pas tous les composants en mémoire sans besoin réel.

### À toi

Construis trois onglets. Saisis du texte dans le premier, passe au deuxième puis reviens. Observe si l'état est perdu ; ajoute `KeepAlive` seulement si tu veux conserver cet état.

---

## 8. API calls — communiquer avec un serveur

### Les états à distinguer

Une requête n'est pas seulement « données présentes ou absentes ». Une interface fiable distingue :
1. **idle** : aucune requête en cours ;
2. **loading** : la requête est en cours ;
3. **success** : données reçues et utilisables ;
4. **empty** : succès, mais aucun résultat ;
5. **error** : échec HTTP, réseau ou traitement.

### Exemple complet avec `fetch`

```vue
<script setup>
import { onMounted, ref } from 'vue'

const plats = ref([])
const chargement = ref(false)
const erreur = ref('')

async function chargerPlats() {
  chargement.value = true
  erreur.value = ''

  try {
    const reponse = await fetch('/api/plats')

    // fetch ne rejette pas automatiquement les réponses HTTP 404/500.
    if (!reponse.ok) {
      throw new Error(`La requête a échoué : HTTP ${reponse.status}`)
    }

    const donnees = await reponse.json()
    if (!Array.isArray(donnees)) {
      throw new Error('Le format reçu est incorrect.')
    }

    plats.value = donnees
  } catch (cause) {
    erreur.value = cause instanceof Error
      ? cause.message
      : 'Une erreur inconnue est survenue.'
  } finally {
    chargement.value = false
  }
}

onMounted(chargerPlats)
</script>

<template>
  <p v-if="chargement" role="status">Chargement des plats…</p>
  <p v-else-if="erreur" role="alert">{{ erreur }}</p>
  <p v-else-if="plats.length === 0">Aucun plat disponible.</p>
  <ul v-else>
    <li v-for="plat in plats" :key="plat.id">
      {{ plat.nom }} — {{ plat.prix }} FCFA
    </li>
  </ul>

  <button type="button" @click="chargerPlats">Actualiser</button>
</template>
```

Le chemin `/api/plats` est un exemple à adapter à ton backend. En production, définis clairement l'URL de l'API, le contrat JSON et la forme des erreurs. Ne fais jamais confiance à une réponse réseau sans vérifier les champs dont l'interface a besoin.

### Où placer le code HTTP ?

Quand une requête devient réutilisée ou complexe, place-la dans `services/platsApi.js`, puis appelle le service depuis un composable ou un store. Le service connaît HTTP ; le composant connaît l'interface. Évite de recopier la même logique de gestion d'erreur dans dix composants.

### À toi

Ajoute une recherche, une erreur simulée, un bouton de nouvelle tentative et un affichage vide. Vérifie séparément erreur réseau et réponse HTTP 500.

---

## 9. Vue Router — navigation côté client

### Le rôle du routeur

Une application monopage peut afficher plusieurs pages sans recharger entièrement le document. Vue Router relie une URL à une vue. Les trois notions de départ :
- `RouterLink` : lien de navigation ;
- `RouterView` : emplacement de la page active ;
- configuration des routes : correspondance entre chemins et composants.

### Exemple minimal

```js
// src/router/index.js
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'catalogue',
    component: () => import('../views/CatalogueView.vue')
  },
  {
    path: '/plats/:id',
    name: 'plat-detail',
    component: () => import('../views/PlatDetailView.vue'),
    props: true
  },
  {
    path: '/commandes',
    name: 'commandes',
    component: () => import('../views/CommandesView.vue')
  },
  {
    path: '/:pathMatch(.*)*',
    name: 'not-found',
    component: () => import('../views/NotFoundView.vue')
  }
]

export default createRouter({
  history: createWebHistory(),
  routes
})
```

```js
// src/main.js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'
import router from './router'

createApp(App).use(createPinia()).use(router).mount('#app')
```

Dans `App.vue`, le layout général contient `<RouterView />`. Les liens utilisent `<RouterLink to="/commandes">Commandes</RouterLink>`. Pour un détail, préfère une navigation nommée avec un paramètre plutôt que de concaténer des URLs au hasard.

### Paramètres, query et guards

- Paramètre de route : `/plats/42`, par exemple l'identifiant du plat.
- Query string : `/plats?categorie=boissons`, souvent utile pour recherche, filtre ou pagination.
- Guard : vérifie une condition de navigation et peut rediriger. Il améliore le parcours, mais ne sécurise pas une API : le serveur doit toujours contrôler les droits.

Avec `createWebHistory`, configure l'hébergement pour renvoyer les chemins inconnus vers `index.html`, sinon le rechargement direct d'une URL profonde peut donner une 404 du serveur.

### À toi

Crée Catalogue, Détail, Commandes et 404. Teste les liens, retour navigateur, actualisation sur une URL profonde, paramètre absent et identifiant inconnu.

---

## 10. Pinia — état partagé entre plusieurs composants

### Quand en avoir besoin ?

Un état local appartient à un composant. Un état peut être placé dans Pinia quand plusieurs pages ou composants doivent partager les mêmes données et actions : panier, session d'interface ou filtres globaux. Tout ne doit pas aller dans un store : un champ de formulaire isolé peut rester local.

### Exemple : store panier

```js
// src/stores/panier.js
import { computed, ref } from 'vue'
import { defineStore } from 'pinia'

export const usePanierStore = defineStore('panier', () => {
  const lignes = ref([])

  const nombreArticles = computed(() =>
    lignes.value.reduce((total, ligne) => total + ligne.quantite, 0)
  )

  const total = computed(() =>
    lignes.value.reduce(
      (somme, ligne) => somme + ligne.prixUnitaire * ligne.quantite,
      0
    )
  )

  function ajouter(plat) {
    const ligne = lignes.value.find(item => item.id === plat.id)
    if (ligne) {
      ligne.quantite++
    } else {
      lignes.value.push({
        id: plat.id,
        nom: plat.nom,
        prixUnitaire: plat.prix,
        quantite: 1
      })
    }
  }

  function vider() {
    lignes.value = []
  }

  return { lignes, nombreArticles, total, ajouter, vider }
})
```

Le store centralise les lignes et les opérations. Les getters calculés (`computed`) dérivent le nombre d'articles et le total : on ne stocke pas une deuxième copie du total qui pourrait devenir incohérente. Dans le composant, appelle `const panier = usePanierStore()` puis `panier.ajouter(plat)`.

### Règles importantes

- Installe Pinia une fois dans l'application avec `.use(createPinia())`.
- Un store est une source de vérité côté interface, pas une base de données ni une garantie de sécurité.
- Le backend doit recalculer les prix, vérifier les stocks et valider une commande.
- Ne destructure pas directement des propriétés réactives d'un store si tu veux conserver leur réactivité : utilise `storeToRefs(store)` pour les états/getters, et garde les actions sur le store.
- La persistance n'est pas automatique par défaut. Si tu ajoutes du stockage local, définis ce qui peut y être conservé et comment gérer les données obsolètes.

### À toi

Utilise le panier depuis deux pages différentes. Vérifie que le nombre et le total sont cohérents après ajout, changement de quantité et suppression.

---

## 11. Formulaires et `useForm`

### D'abord : que signifie `useForm` ?

Vue n'inclut pas de fonction officielle universelle appelée `useForm` dans son cœur. Le nom est utilisé par différentes bibliothèques. Dans ce cours, nous prendrons **VeeValidate** comme exemple, qui fournit un composable `useForm` pour gérer valeurs, erreurs, validation et soumission. D'autres outils peuvent employer le même nom avec des API différentes : vérifie toujours l'import et la documentation de la bibliothèque réellement installée.

### Quand utiliser une bibliothèque ?

Pour un petit formulaire, `ref`, `v-model` et une validation simple peuvent suffire. Pour des formulaires avec plusieurs champs, schémas, erreurs serveur, champs imbriqués ou composants réutilisables, une bibliothèque peut éviter de réécrire la gestion des erreurs et des états.

### Exemple avec VeeValidate

Installation dans un projet de pratique :
```bash
npm install vee-validate
```

```vue
<script setup>
import { useForm } from 'vee-validate'

const { defineField, errors, handleSubmit, isSubmitting, resetForm } = useForm({
  initialValues: {
    nom: '',
    telephone: ''
  },
  validate(values) {
    const erreurs = {}

    if (!values.nom.trim()) erreurs.nom = 'Le nom est obligatoire.'
    if (!/^7[05678]\d{7}$/.test(values.telephone)) {
      erreurs.telephone = 'Saisis un numéro mobile valide.'
    }

    return { errors: erreurs }
  }
})

const [nom, nomAttrs] = defineField('nom')
const [telephone, telephoneAttrs] = defineField('telephone')

const soumettre = handleSubmit(async (values) => {
  // Ici, appelle ton service API et gère les erreurs renvoyées par le serveur.
  console.log('Données validées :', values)
  resetForm()
})
</script>

<template>
  <form @submit="soumettre">
    <label for="nom">Nom</label>
    <input id="nom" v-model="nom" v-bind="nomAttrs" autocomplete="name">
    <p v-if="errors.nom" role="alert">{{ errors.nom }}</p>

    <label for="telephone">Téléphone</label>
    <input
      id="telephone"
      v-model="telephone"
      v-bind="telephoneAttrs"
      inputmode="tel"
      autocomplete="tel"
    >
    <p v-if="errors.telephone" role="alert">{{ errors.telephone }}</p>

    <button type="submit" :disabled="isSubmitting">
      {{ isSubmitting ? 'Envoi…' : 'Commander' }}
    </button>
  </form>
</template>
```

Cet exemple illustre les rôles, mais vérifie la version de VeeValidate installée : la configuration des schémas et les signatures peuvent varier selon la version. Le numéro de téléphone est une règle d'exemple, à adapter aux numéros que ton application accepte.

### Validation frontend et backend

La validation frontend améliore l'expérience, mais ne suffit jamais à protéger les données. Le backend doit revalider tous les champs. Les erreurs serveur (par exemple un stock épuisé ou un numéro déjà utilisé) doivent être affichées clairement sans effacer inutilement la saisie.

### À toi

Ajoute nom, téléphone, adresse et lignes commandées. Gère les champs obligatoires, une soumission en cours, une erreur de serveur, une réussite et la réinitialisation uniquement après réussite.

---

## 12. Comment ces outils travaillent ensemble

Pour une application de restaurant maintenable, un flux raisonnable pourrait être :

1. **Vue Router** choisit la page selon l'URL.
2. La page utilise un **composable** ou un **store Pinia** selon qu'elle partage ou non l'état.
3. Un **service API** effectue la requête HTTP et vérifie le contrat de réponse.
4. Le composant affiche chargement, erreur, état vide ou données.
5. Les **watchers** réagissent aux changements qui doivent déclencher un effet secondaire, par exemple une recherche.
6. Les **computed** calculent les valeurs dérivées, comme le total du panier.
7. Les **lifecycle hooks** démarrent et nettoient les ressources liées au composant.
8. Les **template refs** et **directives** sont réservées aux besoins DOM particuliers.
9. Les **composants asynchrones** ou le lazy loading du routeur réduisent le code chargé initialement quand cela est pertinent.
10. **VeeValidate `useForm`** peut gérer un formulaire complexe ; l'API serveur garde la responsabilité des règles métier.

Tu n'as pas besoin d'utiliser toutes ces techniques dans chaque projet. Une bonne architecture est la plus simple qui respecte les besoins réels.

## Tableau de décision rapide

| Si tu veux… | Commence par… |
|---|---|
| Calculer le total du panier | `computed` |
| Réagir à une valeur et lancer une requête | `watch` |
| Mettre le focus ou mesurer un élément DOM | template ref |
| Démarrer/arrêter un timer lié à un composant | lifecycle hooks |
| Réutiliser une logique réactive | composable |
| Partager un panier entre pages | Pinia |
| Associer une URL à une page | Vue Router |
| Charger le code d'une page à la demande | lazy loading du routeur |
| Choisir dynamiquement un onglet/composant | `<component :is>` |
| Ajouter un comportement DOM bas niveau réutilisable | directive personnalisée |
| Gérer un formulaire complexe | bibliothèque comme VeeValidate `useForm` |
| Obtenir des données du serveur | service API avec `fetch` et états explicites |

## Vérification de maîtrise

Sans regarder le texte, explique avec tes propres mots :
1. Pourquoi `computed` n'est pas un remplacement de `watch`.
2. Pourquoi une template ref est souvent `null` avant le montage.
3. Pourquoi une réponse HTTP 404 ne suffit pas à faire échouer `fetch`.
4. Pourquoi un guard du routeur ne protège pas les données du backend.
5. Pourquoi le total du panier doit être calculé et le prix revérifié par le serveur.
6. La différence entre composable, service et store.
7. Quand préférer une route lazy-loaded à un composant asynchrone local.
8. Pourquoi une directive personnalisée ne doit pas remplacer un composant métier.
9. Ce que fournit VeeValidate `useForm` et ce qu'il ne remplace pas.
10. Comment nettoyer un timer ou annuler une requête qui n'est plus utile.

Tu as compris si tu peux aussi construire chaque exemple, le modifier, expliquer ses limites et diagnostiquer un cas d'erreur.
