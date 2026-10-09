# Méthode de résolution de problèmes frontend

Le développeur professionnel clarifie le besoin, choisit une conception, vérifie le résultat et sait expliquer ses décisions.

## Méthode en 7 étapes

### 1. Reformuler
Écris une phrase décrivant le comportement attendu, sans parler encore de Vue.
Exemple : « Quand le client clique sur Ajouter, le plat rejoint le panier et le total se met à jour. »

### 2. Décrire les données
Note les objets nécessaires, leurs propriétés, leurs types et leurs relations.
- Quel est l'identifiant stable ?
- Quelle donnée est la source de vérité ?
- Quelle valeur peut être calculée ?
- Quelles données peuvent manquer ?

### 3. Décrire les actions
| Action | Donnée concernée | Résultat attendu |
|---|---|---|
| Rechercher | Texte de recherche | Liste filtrée |
| Ajouter au panier | Plat et panier | Quantité mise à jour |
| Retirer | Identifiant du plat | Ligne supprimée |
| Recharger | Données persistées | État restauré ou valeur initiale |

### 4. Découper
Sépare le problème en petites tâches testables. Commence par le cas simple, puis ajoute règles et cas limites.

### 5. Prédire
Avant d'exécuter, écris ce que tu penses voir. Compare la prédiction au résultat.

### 6. Vérifier les cas limites
Teste au minimum : liste vide, identifiant inconnu, quantité invalide, champ rempli d'espaces, réponse API lente, réseau indisponible, double clic, données locales mal formées, petit écran et navigation clavier.

### 7. Expliquer
Sans regarder le code, explique :
- pourquoi la donnée est réactive ;
- où l'état est possédé ;
- pourquoi tu as choisi computed, méthode, watch ou composant ;
- comment tu as testé le comportement ;
- ce que tu améliorerais si le projet grandissait.

## Diagnostic par symptôme

| Symptôme | Pistes à vérifier |
|---|---|
| L'écran ne change pas | La donnée est-elle réactive ? La bonne propriété change-t-elle ? |
| undefined ou erreur de lecture | L'objet existe-t-il ? La réponse API est-elle arrivée ? |
| Valeur affichée ancienne | Est-elle dérivée de la source de vérité ? Existe-t-il une copie désynchronisée ? |
| Liste incorrecte après suppression | Les clés sont-elles stables ? L'index sert-il d'identité ? |
| L'enfant modifie une prop | Revoir le contrat props/émits et la responsabilité de l'état |
| Requête échouée sans message | Vérifier response.ok, réseau et états loading/error |
| Build réussi mais page cassée | Vérifier imports, routes, données réelles et console navigateur |
| Test isolé réussi, suite échouée | Vérifier nettoyage, état partagé et dépendance à l'ordre |
| Route privée visible | Le backend doit aussi vérifier les autorisations |
| Fonctionnalité disponible seulement après rafraîchissement | Vérifier mises à jour réactives et source de données |

## Demander de l'aide efficacement
Prépare le résultat attendu, le résultat réel, les étapes de reproduction, l'erreur complète, le code minimal pertinent et ce que tu as déjà essayé. « Ça ne marche pas » ne donne pas assez d'informations pour diagnostiquer.

## Exercice
Choisis un bug de ton application. Écris ton hypothèse avant la correction, reproduis le problème, corrige une seule cause, puis prouve que le bug est résolu et qu'un autre parcours n'a pas régressé.