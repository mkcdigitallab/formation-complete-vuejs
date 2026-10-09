# Module 14 — Intégration Laravel et déploiement

## Contrat frontend/backend
Le frontend présente l'interface et collecte les actions. Le backend Laravel demeure responsable de la validation métier, de l'autorisation, de la persistance et des secrets. Définis clairement les formats de requête/réponse, les codes HTTP et le format des erreurs.

## Points à gérer
- URL de l'API selon l'environnement.
- Authentification conforme au mécanisme choisi.
- CORS et cookies selon le domaine et le déploiement.
- Erreurs de validation Laravel affichées près des champs.
- Pagination, filtres et tri.
- États loading/success/error/empty.
- Expiration de session et réponses 401/403.
- Ne pas supposer qu'un bouton masqué signifie que l'utilisateur n'a pas le droit d'appeler l'API.

## Environnements
Distingue développement, tests et production. Les variables incluses dans le bundle frontend sont publiques. Ne place jamais des identifiants de base de données ou des clés privées dans le frontend.

## Build et publication
- Installer les dépendances de façon reproductible.
- Exécuter lint et tests.
- Exécuter le build de production.
- Vérifier les chemins, routes et variables publiques.
- Déployer et contrôler les parcours critiques.
- Documenter le rollback et la manière de diagnostiquer une erreur.

## Laboratoire final
Connecte ton frontend à une API Laravel :
1. liste les produits ;
2. affiche les erreurs de validation ;
3. crée et modifie une ressource ;
4. gère une session selon l'architecture fournie ;
5. teste les réponses 401, 403, 422 et 500 ;
6. documente les variables d'environnement sans publier de secrets ;
7. lance les tests et le build ;
8. déploie puis vérifie le parcours principal.

## Définition de terminé
Le projet est terminé lorsque l'installation est documentée, le build passe, les tests utiles passent, les cas d'erreur sont gérés et tu peux expliquer le flux de données du navigateur au serveur.
