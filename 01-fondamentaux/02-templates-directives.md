# Module 02 — Templates et directives

## Objectifs
Afficher des données, réagir aux interactions et contrôler le rendu d'une interface.

## Interpolation
Dans le template, `{{ expression }}` affiche une valeur. Les expressions doivent rester simples : l'affichage et la logique complexe ne doivent pas être mélangés.

## Directives essentielles
- `v-bind:href` ou `:href` : lie un attribut à une expression.
- `v-on:click` ou `@click` : écoute un événement.
- `v-if / v-else-if / v-else` : crée ou retire conditionnellement un bloc.
- `v-show` : garde l'élément dans le DOM et modifie sa visibilité CSS.
- `v-for` : répète un élément pour chaque élément d'une collection.
- `v-model` : synchronise un champ de formulaire avec une donnée.

## v-if ou v-show ?
Utilise `v-if` quand le bloc doit réellement exister seulement sous certaines conditions. Utilise `v-show` si l'élément est souvent masqué/affiché et que garder son DOM est utile. Ce ne sont pas des synonymes.

## v-for et key
Une clé stable aide Vue à associer chaque élément de la liste à la bonne identité quand la liste change. Préfère un identifiant durable, par exemple `plat.id`, plutôt que l'index si la liste peut être réordonnée ou supprimée.

## Événements
Les gestionnaires d'événements déclenchent une action. Un modificateur tel que `.prevent` peut prévenir le comportement par défaut d'un formulaire. Utilise les modificateurs lisibles plutôt que des manipulations DOM manuelles.

## Laboratoire — Catalogue
Crée un catalogue de plats avec pour chaque plat un identifiant, un nom, un prix et une quantité disponible.
- Affiche les plats dans une liste.
- Affiche « Rupture » si la quantité est nulle.
- Affiche le prix formaté.
- Ajoute un bouton pour augmenter ou diminuer la quantité.
- Empêche la quantité de devenir négative.
- Ajoute un champ de recherche.
- Affiche un message adapté si aucun plat ne correspond.
- Ajoute un bouton qui montre/cache les détails.

Ne demande pas à un agent d'écrire le laboratoire. Fais d'abord le comportement, puis améliore le CSS.

## Questions
1. Quelle différence entre `v-if` et `v-show` ?
2. Pourquoi une clé stable est-elle importante dans `v-for` ?
3. Quand utiliser `v-bind` ?
4. À quoi sert `v-model` ?

## Critères de réussite
L'interface fonctionne quand la liste est vide, quand un plat est en rupture et quand la recherche ne retourne aucun résultat.
