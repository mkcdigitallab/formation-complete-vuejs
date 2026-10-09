# Guide de l'apprenant

## Méthode pour chaque notion
1. **Besoin :** quel problème réel faut-il résoudre ?
2. **Prédiction :** avant d'exécuter, que penses-tu qu'il va se passer ?
3. **Essai :** écris une petite expérience, sans copier une solution.
4. **Observation :** lis le résultat et la console.
5. **Explication :** décris le mécanisme avec tes propres mots.
6. **Variation :** change une condition et prédis le résultat.
7. **Réutilisation :** applique la notion dans un autre contexte.
8. **Bilan :** note l'erreur rencontrée et comment tu l'as diagnostiquée.

## Questions à se poser avant de coder
- Quelle donnée existe et qui en est responsable ?
- Cette donnée est-elle locale, dérivée, partagée ou fournie par le serveur ?
- Quel composant possède l'état ?
- Quel événement déclenche le changement ?
- Quelle partie du code doit seulement afficher les données ?
- Que se passe-t-il si la liste est vide, si la requête échoue ou si l'utilisateur saisit une valeur invalide ?
- Comment vérifier que le comportement fonctionne ?

## Discipline Git
- Commence par `git status`.
- Une branche par fonctionnalité ou exercice conséquent.
- Des commits petits, compréhensibles et cohérents.
- Lis `git diff` avant de committer.
- Ne pousse pas de secrets, fichiers `.env`, `node_modules` ou fichiers de build inutiles.
- N'écrase jamais un travail existant sans comprendre le diff.

## Règle d'aide
Demande d'abord un indice, puis une explication. N'affiche la correction complète qu'après une tentative documentée. Quand tu reçois une correction, explique-la ensuite sans la regarder.

## Quand considérer une notion acquise ?
Tu peux la définir simplement, expliquer son utilité, l'utiliser sans modèle, reconnaître au moins une erreur fréquente, et l'appliquer dans un exercice nouveau.
