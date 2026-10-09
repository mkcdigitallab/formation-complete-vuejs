# Astuces, pièges et réflexes Vue 3

Ce document accompagne les laboratoires. Essaie d'abord de diagnostiquer par toi-même.

## 1. Réactivité : choisir le bon outil

### ref()
- Dans le script, lis ou modifies la valeur d'un ref avec .value.
- Dans le template, Vue déballe généralement automatiquement un ref de premier niveau.
- Un ref peut représenter une valeur simple, un tableau ou un objet.
- Piège : oublier .value dans le script ou confondre l'objet Ref avec sa valeur.

### reactive()
- Convient à un objet réactif dont tu modifies les propriétés.
- Évite de remplacer l'objet entier si ton code dépend de la référence réactive d'origine.
- La déstructuration d'une propriété primitive peut rompre le lien réactif. Étudie toRefs et toRef quand tu en as réellement besoin.
- Ne choisis pas entre ref et reactive par habitude : explique ton choix.

### computed, méthode ou watch ?
- computed : une valeur dérivée d'autres données. Elle doit généralement rester sans effet secondaire.
- méthode : une action ou un calcul exécuté lorsqu'on l'appelle.
- watch : réagir à un changement pour réaliser un effet secondaire, par exemple sauvegarder ou lancer une requête.
- Si tu maintiens manuellement un total déjà calculable à partir du panier, tu risques de désynchroniser les données.
- Une valeur computed est mise en cache jusqu'au changement de ses dépendances.

## 2. Templates et listes
- Chaque élément de v-for doit avoir une clé stable, généralement un identifiant unique. Évite l'index si la liste peut être triée ou modifiée.
- Évite de mélanger v-if et v-for sur le même élément ; prépare plutôt la liste avec computed.
- v-if crée ou détruit une partie de l'interface ; v-show change sa visibilité.
- v-bind lie une donnée à un attribut ; v-on écoute un événement.
- Si une expression du template devient difficile à lire, déplace la logique dans computed ou une fonction nommée.

## 3. Parent, enfant et données
- Le parent transmet des données avec les props ; l'enfant annonce une intention avec un événement émis.
- Ne modifie pas directement une prop dans l'enfant. L'état appartient au composant responsable de cette donnée.
- Demande-toi toujours : « Qui est la source de vérité ? »
- Un slot permet au parent de fournir du contenu à une zone prévue par l'enfant.
- Découpe un composant lorsqu'une responsabilité claire est à isoler ou réutiliser, pas uniquement pour réduire le nombre de lignes.

## 4. API et asynchronisme
- fetch ne rejette pas automatiquement une promesse pour un statut HTTP comme 404 ou 500. Vérifie response.ok.
- Prévois les états chargement, succès, succès sans résultat et erreur.
- Une liste vide n'est pas une erreur réseau.
- Une requête ancienne peut finir après une requête récente. Étudie AbortController et le nettoyage des watchers.
- Ne place jamais un secret serveur dans une variable d'environnement publique du frontend.

## 5. Formulaires
- Le frontend améliore l'expérience utilisateur ; le backend doit valider à nouveau les données.
- Associe chaque champ à un label explicite.
- Affiche les erreurs près du champ et explique comment corriger.
- Teste chaînes vides, espaces, zéro, valeurs négatives, valeurs trop grandes et caractères inattendus.
- N'utilise pas seulement la couleur pour signaler une erreur.

## 6. Persistance et état
- localStorage stocke des chaînes : sérialise en JSON et gère l'absence ou un JSON invalide.
- Le stockage navigateur n'est pas une base de données ni un emplacement sûr pour les secrets.
- État local : utile à un seul composant.
- État partagé : utile lorsque plusieurs composants ont besoin de la même source de vérité.
- État d'URL : utile pour les recherches, filtres et pages qu'on veut partager ou retrouver avec le bouton retour.
- Pinia ne remplace pas le serveur : le backend reste la source de vérité des données persistantes.

## 7. Déboguer sans paniquer
1. Reproduis le bug avec le scénario le plus petit possible.
2. Lis le premier message pertinent de la console, pas seulement le dernier.
3. Identifie le fichier et la ligne.
4. Observe la valeur réelle avec les outils du navigateur.
5. Formule une hypothèse unique.
6. Change une seule chose puis reteste.
7. Vérifie le cas normal et un cas limite.
8. Note la cause, pas uniquement la correction.

Ne modifie pas cinq fichiers à la fois sans savoir quelle modification résout le problème.

## 8. Avant chaque commit
- [ ] Le comportement demandé fonctionne.
- [ ] Les erreurs et états vides sont gérés.
- [ ] Aucun secret ou fichier généré inutile n'est ajouté.
- [ ] Les noms décrivent l'intention.
- [ ] Le diff a été relu.
- [ ] Les tests pertinents et le build passent.
- [ ] Je peux expliquer ce que j'ai modifié et pourquoi.

## Règle d'or
Quand tu bloques, reformule le problème, identifie la donnée, le déclencheur et le résultat attendu, puis construis une petite expérience pour vérifier ton hypothèse.