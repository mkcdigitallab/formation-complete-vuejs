# Module 08 — Pinia et état partagé

## Pourquoi un store ?
Quand plusieurs composants ont besoin des mêmes données et actions, un store centralisé peut éviter de transmettre des props à travers de nombreuses couches. Mais toutes les données ne doivent pas être globales.

## Concepts Pinia
- State : données possédées par le store.
- Getter : valeur dérivée du state.
- Action : opération métier ou mise à jour.
- Store : ensemble cohérent d'état et d'opérations.
- Plusieurs stores : séparer les responsabilités lorsque le domaine le justifie.

## Où placer l'état ?
- État local : ouverture d'un menu, champ temporaire.
- URL : page courante, filtre partageable ou recherche.
- Serveur : données persistées et faisant autorité.
- Store : données partagées entre plusieurs zones de l'interface, comme un panier local.

Évite de copier toutes les réponses API dans un store global sans besoin clair. Définis la stratégie de rafraîchissement et d'erreur.

## Persistance
La persistance locale est adaptée à certaines préférences ou à un panier non sensible. Elle ne sécurise pas les données : l'utilisateur peut les modifier. Ne stocke pas de secrets ou de données sensibles dans le stockage navigateur sans conception de sécurité appropriée.

## Laboratoire
Crée un store de panier :
- ajouter un article ;
- changer sa quantité ;
- retirer un article ;
- calculer le total ;
- vider le panier ;
- tester les cas limites ;
- conserver le panier après rechargement si cette fonctionnalité est demandée.

Explique quelles données restent dans le composant et lesquelles doivent être partagées.
