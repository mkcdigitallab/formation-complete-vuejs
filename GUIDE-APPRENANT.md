# Guide de l'apprenant

## La règle principale

Le cours doit t'apprendre la notion avant de te demander de l'utiliser. Tu ne dois pas avoir besoin de quitter le dépôt pour chercher la définition d'un mot employé dans une leçon.

Chaque leçon complète doit présenter :
1. **Le besoin concret** : quel problème cette notion résout-elle ?
2. **Le vocabulaire** : expliquer les termes techniques avant de les utiliser.
3. **Le mécanisme** : ce qui se passe réellement et pourquoi.
4. **Un exemple commenté** : expliquer le rôle de chaque partie importante.
5. **Les comparaisons utiles** : par exemple `href` contre `:href`, `ref` contre `reactive`, ou `computed` contre `watch`.
6. **Les erreurs fréquentes** : comment les reconnaître et les diagnostiquer.
7. **La pratique guidée** : une tâche qui réutilise la notion sans fournir directement toute la solution.
8. **L'auto-évaluation** : des questions auxquelles l'apprenant peut répondre après avoir étudié le contenu.

Une question de contrôle ne doit jamais remplacer une explication manquante. Si un terme apparaît pour la première fois, définis-le. Si une syntaxe diffère d'une autre, explique la différence avant de demander à l'apprenant de choisir.

## Méthode de travail pour chaque notion

1. **Comprendre le besoin** : reformule le problème en langage simple.
2. **Prédire** : avant d'exécuter, dis ce que tu penses qu'il va se passer.
3. **Expérimenter** : écris une petite expérience sans recopier une solution complète.
4. **Observer** : compare le résultat à ta prédiction et lis la console si nécessaire.
5. **Expliquer** : décris le mécanisme avec tes propres mots.
6. **Varier** : change une donnée ou une condition et prédis le nouveau résultat.
7. **Réutiliser** : applique la notion dans un autre contexte.
8. **Faire le bilan** : note l'erreur rencontrée et comment tu l'as diagnostiquée.

## Questions à se poser avant de coder

- Quel problème utilisateur dois-je résoudre ?
- Quelles données sont nécessaires et qui en est responsable ?
- Cette donnée est-elle locale, dérivée, partagée ou fournie par le serveur ?
- Quel composant possède l'état ?
- Quelle action déclenche le changement ?
- Quelle partie du code doit seulement afficher les données ?
- Que se passe-t-il si la liste est vide, si la requête échoue ou si l'utilisateur saisit une valeur invalide ?
- Comment vérifier que le comportement fonctionne ?
- Puis-je expliquer pourquoi j'ai choisi cet outil plutôt qu'une alternative ?

## Discipline Git

- Commence par `git status`.
- Une branche par fonctionnalité ou exercice conséquent.
- Des commits petits, compréhensibles et cohérents.
- Lis `git diff` avant de committer.
- Ne pousse pas de secrets, fichiers `.env`, `node_modules` ou fichiers de build inutiles.
- N'écrase jamais un travail existant sans comprendre le diff.

## Comment demander ou recevoir de l'aide

L'objectif n'est pas de cacher les réponses : c'est de construire ta compréhension. Le cours doit d'abord expliquer la notion et montrer un exemple commenté. Pour les exercices, essaie d'abord seul. Si tu bloques, demande un indice ciblé ; après ta tentative, une correction peut être étudiée, mais tu dois ensuite pouvoir expliquer chaque décision et refaire une variante sans la regarder.

Une réponse pédagogique ne doit pas seulement dire « utilise cette syntaxe ». Elle doit expliquer ce que la syntaxe signifie, pourquoi elle convient, dans quel cas elle ne conviendrait pas et comment vérifier son fonctionnement.

## Quand considérer une notion acquise ?

Tu peux :
- la définir simplement ;
- expliquer le problème qu'elle résout ;
- expliquer le fonctionnement d'un exemple ;
- l'utiliser sans modèle ;
- reconnaître au moins une erreur fréquente ;
- choisir entre deux outils proches et justifier ton choix ;
- l'appliquer dans un exercice nouveau.
