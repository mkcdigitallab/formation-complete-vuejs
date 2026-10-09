# LAB 00 — Préparer l'environnement et lire un projet Vue

**Durée indicative :** 60 à 90 minutes.

## Objectifs
Créer un projet Vue, démarrer le serveur, reconnaître les fichiers importants et expliquer le rôle de npm et Vite.

## Partie A — Installation
1. Vérifie les versions de Node.js, npm et Git.
2. Si une dépendance exige une version plus récente de Node, lis l'avertissement et compare les versions requises avant de continuer.
3. Crée un projet avec l'outil officiel create-vue.
4. Pour apprendre progressivement, commence en JavaScript et évite les options avancées que tu n'as pas encore étudiées.
5. Installe les dépendances puis démarre le serveur de développement.
6. Ouvre l'adresse locale affichée dans le terminal.

## Partie B — Exploration guidée
Repère et explique :
- package.json : scripts et dépendances ;
- fichier HTML d'entrée ;
- src/main.js : point d'entrée JavaScript ;
- src/App.vue : composant racine ;
- src/components/ : composants ;
- styles ;
- node_modules/ : dépendances installées, à ne pas committer ;
- package-lock.json : versions résolues.

Explique comment l'application passe du point d'entrée au composant affiché dans le navigateur.

## Partie C — Expériences
1. Change un texte et observe le navigateur.
2. Provoque une faute de syntaxe, lis le message, puis répare-la.
3. Crée un composant très simple et affiche-le depuis le composant racine.
4. Arrête le serveur avec Ctrl+C puis redémarre-le.
5. Lis le script dev dans package.json et explique la commande lancée.

## Partie D — Git
1. Vérifie git status.
2. Consulte git diff.
3. Crée un commit au message explicite.
4. Vérifie l'historique.

## Critères d'acceptation
- [ ] Le serveur démarre sans erreur bloquante.
- [ ] Je sais où se trouve le composant racine.
- [ ] Je modifie l'interface et j'observe le résultat.
- [ ] Je retrouve une erreur dans la console ou le terminal.
- [ ] Je peux expliquer la différence entre Node.js, npm, Vite et Vue.
- [ ] Je sais vérifier les changements avant un commit.

## Questions orales
1. Vue est-il un langage de programmation ?
2. Pourquoi utiliser un serveur de développement ?
3. Quelle différence entre installer une dépendance et lancer le serveur ?
4. Quel fichier indiquer à quelqu'un qui veut démarrer le projet ?

## Extension
Écris un README contenant les commandes d'installation, de démarrage et les difficultés rencontrées.