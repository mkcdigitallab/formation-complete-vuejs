# Module 04 — Composants, props, emits et slots

## Pourquoi découper ?
Un composant représente une partie d'interface ayant un rôle clair. Le découpage facilite la réutilisation, les tests et la lecture. Trop de petits composants inutiles rendent aussi le projet difficile : découpe en fonction des responsabilités.

## Props : parent vers enfant
Le parent possède souvent les données et les transmet à l'enfant via des props. L'enfant les utilise pour afficher son interface. Une prop ne doit pas être modifiée directement par l'enfant : il signale plutôt une intention au parent.

## Emits : enfant vers parent
L'enfant émet un événement nommé lorsque l'utilisateur effectue une action. Le parent écoute cet événement et décide quoi faire. L'enfant n'a pas besoin de connaître toute la logique du parent.

Exemple conceptuel : une carte de plat reçoit les données d'un plat en props et émet `ajouter-au-panier` lorsque l'utilisateur clique. Le parent décide comment mettre à jour le panier.

## Slots
Un slot permet au parent de fournir du contenu personnalisé à l'intérieur d'un composant générique. Les slots nommés permettent plusieurs zones de contenu, par exemple titre et pied de page.

## Cycle de vie
- `onMounted` : après insertion du composant dans le DOM ; utile pour démarrer certains effets ou interagir avec un élément DOM.
- `onUnmounted` : nettoyer timers, abonnements ou écouteurs créés manuellement.
- Les hooks doivent être enregistrés dans le bon contexte de setup.
N'utilise pas le cycle de vie si une simple expression réactive suffit.

## Laboratoire — Carte produit
Crée :
- une page parent qui détient le tableau de produits ;
- une carte enfant qui reçoit un produit par props ;
- un bouton enfant qui émet un événement d'ajout ;
- le parent qui écoute l'événement et met à jour le panier ;
- un compteur affichant le nombre d'articles ;
- un composant de bouton réutilisable avec un slot.

Tu dois pouvoir expliquer pourquoi les données appartiennent au parent et pourquoi l'enfant émet une intention au lieu de modifier directement le tableau parent.

## Questions
1. Quelle direction suivent les props ?
2. Pourquoi émettre un événement ?
3. Quelle différence entre prop et slot ?
4. Quand nettoyer une ressource dans `onUnmounted` ?
