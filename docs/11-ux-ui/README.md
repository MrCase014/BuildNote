# L. UX/UI — À produire en Couche 6

> **Statut : À produire.** Dépend de la validation des Couches 1–3.

Contenu prévu :
- **Architecture de l'information** : navigation séparée pour les deux modules, socle transverse
  (compte, langue, établissement courant).
- **Design system** avec la palette imposée :
  - **Bleu clair** — couleur primaire (actions, navigation, éléments interactifs).
  - **Orange** — couleur d'accent (alertes, mises en avant, appels à l'action secondaires, faible
    confiance OCR).
  - **Blanc** — fond, respiration, lisibilité.
  - Neutres (gris) pour le texte et les bordures ; états sémantiques (succès, avertissement, erreur)
    dérivés sans trahir la palette.
- **Accessibilité** : contrastes AA minimum, tailles de cible tactile, navigation clavier, textes
  alternatifs, compatibilité avec des écrans modestes.
- **i18n FR/EN** : **sélecteur de langue sur l'écran d'accueil**, persistance du choix, i18n de
  tous les contenus (UI, messages, exports, explications d'orientation), architecture non limitée à
  deux langues.
- **Wireframes** des parcours clés :
  - Module 1 : import → revue du formulaire prérempli (score de confiance par cellule, image source
    zoomable) → correction → validation.
  - Module 2 : dashboard de situation (sélection de périmètre, rafraîchissement explicite) ;
    demande d'orientation → dossier explicable (facteurs, poids, alternatives, incertitudes).
  - Interopérabilité : assistant d'import, tableau de bord qualité, quarantaine.
- **Mode faible connectivité / hors-ligne** : indicateurs d'état, file de synchronisation, gestion
  des conflits côté UI.
- **Prototypes cliquables** + **tests d'utilisabilité** avec des utilisateurs représentatifs.

Cadre : [`../04-architecture-fonctionnelle/architecture-fonctionnelle.md`](../04-architecture-fonctionnelle/architecture-fonctionnelle.md),
risque d'adoption [`../16-risques/risques.md`](../16-risques/risques.md) R9.
