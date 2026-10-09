# Module 05 — Formulaires, validation et CRUD

## Objectifs
Construire des formulaires fiables, afficher les erreurs près des champs et gérer création, lecture, modification et suppression.

## Modéliser le formulaire
Avant de créer les champs, définis les données attendues et leurs règles. Distingue :
- la valeur saisie ;
- la valeur validée ;
- le message d'erreur ;
- l'objet métier créé ou modifié.

Les données du formulaire ne doivent pas être considérées comme valides simplement parce que le navigateur a permis la saisie.

## Validation
Pour un produit, vérifie au minimum :
- le nom n'est pas vide après suppression des espaces superflus ;
- le prix est numérique et supérieur ou égal à zéro selon la règle choisie ;
- le stock est un entier et ne devient jamais négatif ;
- les erreurs sont compréhensibles et associées aux champs ;
- le focus et le clavier restent utilisables.

Les attributs HTML comme `required`, `min` et `type="number"` améliorent l'expérience mais ne remplacent pas la validation côté serveur.

## CRUD
- Create : créer un élément valide.
- Read : afficher la collection et le détail.
- Update : charger les données existantes puis sauvegarder les changements.
- Delete : confirmer une suppression destructive et retirer l'élément correspondant.

Conserve une identité stable pour chaque élément. Lors d'une édition, évite de modifier par accident l'objet original avant que l'utilisateur confirme.

## Laboratoire
Crée un formulaire d'administration de plats :
1. Ajouter un plat.
2. Afficher des erreurs pour nom vide et prix invalide.
3. Modifier un plat existant.
4. Annuler une édition sans changer la liste.
5. Supprimer un plat après confirmation.
6. Gérer la liste vide et le message de succès.
7. Tester les cas limites.

## Questions
- Pourquoi faut-il valider côté serveur même si le frontend valide déjà ?
- Quelle différence entre annuler une édition et enregistrer ?
- Pourquoi l'identifiant doit-il rester stable ?
