# M. Proof of Concept (POC) — À produire en Couche 7

> **Statut : À produire.** Les POC sont exécutés en **Phase 6**, avant la décision de construction
> (Phase 7). Ce sont des prototypes **jetables** : ils ne deviennent pas le produit.

Chaque POC est spécifié avec : **objectif · hypothèse à valider · protocole · jeux de données
représentatifs · critères de succès chiffrés · méthode de mesure · résultats · limites ·
recommandation (poursuivre / ajuster / renoncer)**.

## POC 1 — OCR
- **Objectif** : mesurer la qualité de reconnaissance sur des fiches réelles (imprimées et
  manuscrites) dans des conditions de terrain (photos smartphone, éclairage variable).
- **Critères de succès indicatifs** : ≥ 90 % de champs corrects sur imprimé ; ≥ 70 % sur manuscrit
  lisible ; temps de traitement acceptable ; faisabilité hors-ligne évaluée.

## POC 2 — Extraction de tableaux
- **Objectif** : valider la détection de la structure tabulaire (lignes/colonnes/cellules) et
  l'association **élève ↔ ligne**, **matière/colonne ↔ valeur**, sur des gabarits de fiches variés.
- **Critères de succès indicatifs** : structure correctement reconstruite sur ≥ 85 % des fiches
  d'un jeu représentatif ; rapprochement élève correct ≥ 90 %.

## POC 3 — Interopérabilité
- **Objectif** : prouver la chaîne `source externe → connecteur → mapping → normalisation →
  validation → modèle canonique` sur **2–3 systèmes réels** (ex. un SGBD, un export CSV/Excel, une
  ancienne application) ; tester la gestion des conflits et la réversibilité (export).
- **Critères de succès indicatifs** : import d'un établissement type sans développement lourd ;
  taux de quarantaine maîtrisé ; lineage complet ; export canonique réimportable.

## POC 4 — Moteur d'orientation
- **Objectif** : valider la faisabilité d'un scoring **pondéré multi-critères** combinant profil,
  aspirations, avis parents, offre, débouchés et besoins nationaux, **avec explications**, sur des
  cas d'élèves réels anonymisés.
- **Critères de succès indicatifs** : recommandations jugées pertinentes et compréhensibles par des
  conseillers d'orientation ; explications complètes (facteurs, poids, alternatives, incertitudes) ;
  stabilité des résultats.

## Sortie
Les 4 rapports alimentent la **décision de construction (J7)** et le choix définitif des briques
technologiques à risque. Voir [`../15-livrables-par-phase/livrables.md`](../15-livrables-par-phase/livrables.md) (Phases 6 et 7).
