# Module 12 — Accessibilité, sécurité et performance

## Accessibilité
- Utilise des éléments HTML sémantiques.
- Associe les champs à des labels.
- Rends toutes les actions accessibles au clavier.
- Préserve un focus visible et logique.
- Utilise un contraste lisible.
- Ne communique pas une erreur uniquement par la couleur.
- Fournis un texte utile aux images informatives ; laisse les images décoratives ignorables.

## Sécurité frontend
- Tout code exécuté dans le navigateur est visible par l'utilisateur.
- Ne place jamais de clé secrète serveur dans une variable publique ou un bundle.
- Valide les données côté serveur même si le frontend les valide.
- Évite l'injection de HTML non fiable.
- Comprends XSS, CSRF, CORS, cookies et sessions dans le contexte de l'architecture utilisée.
- Garde les dépendances à jour et examine les alertes.
- Les guards de routes et les éléments masqués ne remplacent pas l'autorisation serveur.

## Performance
Mesure avant d'optimiser. Examine la taille du bundle, le chargement des images, le nombre d'éléments DOM et les recalculs inutiles. Utilise le chargement différé pour les routes lourdes si le besoin est réel. Une abstraction ou une optimisation prématurée peut augmenter la complexité sans gain mesurable.

## Laboratoire
Audite un projet de boutique :
- navigue uniquement au clavier ;
- corrige les labels et le focus ;
- recherche les secrets dans les fichiers frontend ;
- vérifie les états d'erreur ;
- mesure le build ;
- identifie une amélioration de performance et justifie-la par une mesure.

## Critères
Tu peux distinguer les protections d'expérience utilisateur des véritables contrôles de sécurité côté serveur.
