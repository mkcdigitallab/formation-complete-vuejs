# Projet 1 — Application de restaurant

## Contexte
Le propriétaire veut consulter le menu, rechercher des plats, vérifier le stock et constituer une commande.

## Règles métier
- Chaque plat possède un identifiant stable, un nom, un prix et une quantité disponible.
- Prix et stock ne peuvent pas être négatifs.
- Une commande ne dépasse pas le stock disponible.
- Une ligne de panier représente un plat et la quantité choisie.
- Sous-total = prix du plat × quantité commandée.
- Total = somme des sous-totaux.
- Le retrait de la dernière ligne affiche l'état panier vide.
- Le filtrage ne modifie pas le catalogue original.

## Écrans
1. Menu : cartes, prix, disponibilité et ajout.
2. Recherche, filtre de rupture de stock et tri par prix.
3. Panier : lignes, quantités, sous-totaux, total et suppression.
4. Gestion des plats : création, modification et suppression avec validation.
5. États vides lorsque le menu, la recherche ou le panier ne contient rien.

## Étapes de réalisation
### A — JavaScript sans Vue
Crée un tableau de plats. Écris des fonctions pour rechercher, filtrer, calculer un sous-total et un total. Teste plusieurs jeux de données.

### B — Affichage
Affiche le catalogue et la disponibilité avec une structure HTML sémantique et des clés stables.

### C — Réactivité
Ajoute recherche, filtre et tri. Les résultats affichés doivent être dérivés du catalogue et des critères actifs. Explique le choix de computed.

### D — Panier
Ajoute les actions d'ajout, diminution et suppression. Le stock et les quantités restent cohérents.

### E — Composants
Sépare catalogue, carte de plat et panier lorsque cela clarifie les responsabilités. Transmets les données par props et fais remonter les intentions par événements.

### F — Formulaire
Ajoute création et modification. Affiche les erreurs près des champs et refuse les valeurs invalides.

### G — Persistance et qualité
Sauvegarde le panier localement, gère un JSON invalide et écris des tests pour les calculs et règles de quantité.

## Tests manuels obligatoires
- Catalogue vide.
- Recherche sans résultat.
- Plat en rupture.
- Ajout répété du même plat.
- Tentative de dépasser le stock.
- Prix ou stock invalide.
- Suppression du dernier élément.
- Rechargement de page.
- JSON local incorrect.

## Livrables
Application exécutable, commandes documentées, code lisible, tests, README expliquant les choix et démonstration orale.

## Barème sur 20
- Fonctionnalités et règles métier : 5
- Réactivité et calculs : 4
- Architecture des composants : 3
- Validation et cas limites : 3
- Tests et lisibilité : 3
- Explication et documentation : 2

**Validation :** 14/20 minimum et aucune erreur critique sur le total ou le stock.