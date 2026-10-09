# Fiche de révision Vue 3 — questions à savoir expliquer

Utilise cette fiche pour t'interroger à voix haute. Une réponse correcte doit contenir une définition, un cas d'usage, un exemple concret et une limite.

## Fondamentaux
1. Qu'est-ce qu'un composant Vue ?
2. À quoi servent template, script setup et style dans un fichier .vue ?
3. Quel rôle jouent Node.js, npm et Vite ?
4. Quelle différence entre un événement utilisateur et une modification de donnée ?
5. Pourquoi utiliser une clé stable dans une liste ?

## Réactivité
6. Qu'est-ce qu'une donnée réactive ?
7. Quelle différence entre ref et reactive ?
8. Pourquoi utilise-t-on .value dans le script mais souvent pas dans le template ?
9. Quand utiliser computed plutôt qu'une méthode ?
10. Quand utiliser watch plutôt que computed ?
11. Qu'est-ce qu'un effet secondaire ?
12. Pourquoi le total d'un panier devrait-il généralement être dérivé des lignes ?

## Composants
13. Quelle direction suivent les props ?
14. Pourquoi l'enfant émet-il un événement au lieu de modifier la donnée du parent ?
15. Quand un slot est-il utile ?
16. Qu'est-ce qu'un composant trop complexe ?
17. À quoi sert onUnmounted ?

## Données et architecture
18. Quelle différence entre état local, partagé, URL et serveur ?
19. Quand Pinia est-il utile, et quand ne l'est-il pas ?
20. À quoi sert un composable ?
21. Pourquoi isoler les appels API dans un service ?
22. Pourquoi gérer chargement, erreur, succès et liste vide séparément ?
23. Pourquoi fetch doit-il vérifier response.ok ?
24. Comment éviter une réponse API ancienne qui écrase la plus récente ?

## Qualité et sécurité
25. Quelle différence entre test unitaire, test de composant et test end-to-end ?
26. Comment tester un événement émis ?
27. Pourquoi la validation frontend ne suffit-elle pas ?
28. Pourquoi les variables VITE_* ne sont-elles pas secrètes ?
29. Pourquoi cacher une route ne sécurise-t-il pas l'API ?
30. Que vérifier après un build et un déploiement ?

## Exercice d'entretien
Choisis cinq questions au hasard. Pour chacune :
- réponds sans lire ;
- donne un exemple tiré de ton projet ;
- cite une erreur fréquente ;
- explique comment tu vérifierais le comportement.

Si tu récites une définition sans savoir l'appliquer, la notion n'est pas encore acquise.