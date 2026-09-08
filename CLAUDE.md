# BuildNote — Carte du projet

> Fichier de contexte pour les assistants IA. **`CLAUDE.md` et `AGENTS.md` (racine) ont un contenu
> identique — les modifier ensemble.** À maintenir à jour à chaque changement de structure.

## Nature du projet

BuildNote est une **plateforme d'aide à la décision éducative** (primaire, secondaire, supérieur),
**initiative privée**, ambition **multi-établissements**, contexte **camerounais** (extensible
multi-pays). Deux **modules fonctionnellement séparés** + un socle commun :

1. **Module 1 — Capture & gestion des données académiques** : photo/vidéo d'une fiche → OCR / CV /
   Document Understanding → formulaire prérempli → **vérification humaine OBLIGATOIRE** → validation
   → stockage. L'OCR n'enregistre jamais sans revue humaine.
2. **Module 2 — Orientation** : (a) *dashboard de situation* par classe/établissement, **rafraîchi à
   la demande** ; (b) *orientation individuelle* combinant parcours, résultats, tendances,
   compétences, intérêts, aspirations, **avis des parents**, offre de formation accessible
   (géolocalisée), métiers, et **besoins stratégiques nationaux** → **recommandations explicables**.
   **Aucun recalcul automatique** à l'enregistrement d'une note. Aide à la décision, jamais
   prescription.

Transverse : interopérabilité **par modèle canonique + connecteurs** (jamais « compat SQL
universelle ») ; données en 3 strates **Raw / Normalized / Intelligence** ; **isolation stricte des
établissements** (multi-tenant) ; UI **bilingue FR/EN** (sélecteur dès l'accueil) ; palette **bleu
clair / orange / blanc** ; **faible connectivité** (Module 1 offline-first).

## Règles de travail

- **AUCUNE ligne de code** avant la porte de décision **J7** (après les POC). Le dépôt ne contient
  aujourd'hui que de la **documentation** (`docs/`) et des visuels de marque.
- Documentation **en français** (le produit reste bilingue FR/EN), **Markdown + diagrammes
  Mermaid**, versionnée, revue.
- Production **par couches (1→7) avec porte de validation** entre chacune.
- Chaque document porte un en-tête `Statut` (Brouillon / En revue / Validé) + date.
- Décisions d'architecture tracées en **ADR** dans `docs/17-decisions/`.
- Ne pas réintroduire de MVP jetable : V1 = solution de production, avec **déploiement pilote
  progressif** (1 établissement d'abord).
- Toute demande touchant une **règle non négociable** (validation humaine OCR ; Module 2 sans
  recalcul auto ; dashboard à la demande ; explicabilité ; isolation établissements ;
  interopérabilité par canonique ; FR/EN) = changement **critique** (voir
  `docs/01-project-management/gestion-changements-versions-documentaire.md`).

## Arborescence `docs/`

```
docs/
  README.md                         Index + synthèse exécutive (10 points) — POINT D'ENTRÉE
  00-vision/vision-produit.md        A. Vision, mission, valeur, objectifs, utilisateurs, parties prenantes
  01-project-management/             B. Charter · gouvernance/RACI · méthodologie · roadmap · changements/versions/doc
  02-analyse-metier/                 C. Problématique · besoins (MoSCoW) · AS-IS/TO-BE · personas · cas d'usage UC-01..14
  03-cahier-des-charges/             D. Exigences EF-* / ENF-* · contraintes · critères d'acceptation · KPI · traçabilité
  04-architecture-fonctionnelle/     E. Deux modules séparés + socle + contrats + règles non négociables
  05-architecture-technique/         F. 3 scénarios comparés → recommandation "hybride" + options de composants
  06-architecture-donnees/           G. Raw/Normalized/Intelligence · MCD/MLD/MPD · dictionnaire · versioning schéma
  07-interoperabilite/               H. Modèle canonique · connecteurs · mapping · ETL · conflits · lineage · qualité
  08-ocr-computer-vision/            I. Pipeline 10 étapes (→ validation humaine → stockage) · MLOps · métriques
  09-moteur-orientation/             J. Fusion 6 catégories · scoring additif pondéré · explicabilité · référentiel national
  10-securite/                       K. Authn · RBAC/ABAC · chiffrement · isolation multi-tenant · audit · DPIA · STRIDE
  11-ux-ui/                          L. Architecture UX · design system (bleu clair/orange/blanc) · i18n FR/EN · offline
  12-poc/                            M. Plans des 4 POC (OCR · tableaux · interopérabilité · orientation) — Phase 6
  13-tests/                          O. Stratégie + 11 types de test — Phases 8–9
  14-deploiement/                    P. 6 scénarios + pilote + généralisation par vagues
  15-livrables-par-phase/livrables.md Q. Par phase : objectif/activités/livrables/critères/responsables/dépendances/go-no-go
  16-risques/risques.md              Registre R1..R19 + mitigations (vivant)
  17-decisions/decisions-prealables.md 12 décisions à arbitrer en Phase 2 + modèle d'ADR (vivant)
  glossaire.md                       Terminologie FR (+ EN)
```

## Correspondance couches ↔ phases du cycle de vie

| Couche | Sections | Phases couvertes |
|---|---|---|
| 1 | Vision, archi fonctionnelle, vues d'ensemble données/interop/orientation, roadmap, livrables, risques, décisions | Transverse (cadrage directeur) |
| 2 | Project management complet, analyse métier | Phases 0–1 |
| 3 | Cahier des charges, scénarios d'architecture technique | Phases 2–3 |
| 4 | Données (MCD/MLD/MPD), interopérabilité détaillée | Phase 4 |
| 5 | Pipeline OCR/CV, moteur d'orientation détaillé | Phases 4–5 |
| 6 | Sécurité, UX/UI | Phases 4–5 |
| 7 | POC, tests, déploiement, consolidation des livrables | Phases 6–7 (+ cadrage 9–11) |

Phases : `0` Cadrage · `1` Analyse · `2` Faisabilité + décisions · `3` Spécification · `4`
Conception/architecture · `5` UX/UI · `6` POC · **`7` GO/NO-GO (premier code)** · `8` Développement
(lots L0–L5) · `9` Recette · `10` Pilote (1 étab.) · `11` Généralisation par vagues.

## Où intervenir selon la demande

| La demande porte sur… | Fichier(s) |
|---|---|
| Vision, valeur, périmètre, parties prenantes | `docs/00-vision/vision-produit.md`, `docs/01-project-management/project-charter.md` |
| Planning, jalons, gouvernance, méthode, changements | `docs/01-project-management/` |
| Besoins, processus, personas, cas d'usage | `docs/02-analyse-metier/` |
| Une exigence (fonctionnelle / non fonctionnelle), un KPI | `docs/03-cahier-des-charges/` |
| Séparation des modules, contrats, règles non négociables | `docs/04-architecture-fonctionnelle/architecture-fonctionnelle.md` |
| Choix d'architecture technique, composants, stack | `docs/05-architecture-technique/scenarios-architecture.md` + ADR |
| Modèle de données, entités, MCD/MLD/MPD, strates | `docs/06-architecture-donnees/` |
| Connecteurs, mapping, import/export, conflits, lineage | `docs/07-interoperabilite/` |
| Pipeline OCR/CV, scores de confiance, validation humaine | `docs/08-ocr-computer-vision/pipeline.md` |
| Scoring d'orientation, explicabilité, référentiel national | `docs/09-moteur-orientation/architecture-detaillee.md` |
| Auth, rôles, chiffrement, multi-tenant, RGPD, DPIA | `docs/10-securite/architecture-securite.md` |
| Écrans, design system, palette, i18n, offline UX | `docs/11-ux-ui/architecture-ux-ui.md` |
| Ce qu'il faut prouver avant de coder | `docs/12-poc/plans-poc.md` |
| Comment tester | `docs/13-tests/strategie-tests.md` |
| Comment/où déployer | `docs/14-deploiement/plan-deploiement.md` |
| Livrables et critères de passage d'une phase | `docs/15-livrables-par-phase/livrables.md` |
| Un risque | `docs/16-risques/risques.md` |
| Une décision à arbitrer, un ADR | `docs/17-decisions/decisions-prealables.md` |
| Un terme métier/technique | `docs/glossaire.md` |

## Décisions préalables non tranchées (à arbitrer en Phase 2)

Hébergement/souveraineté · cadre juridique & rétention · stratégie OCR (managé/open source/mixte) ·
modèle multi-tenant · gouvernance du référentiel stratégique national · périmètre V1 · « pas de
MVP » vs pilote progressif · cible de connectivité · modèle économique · stack technologique ·
politique linguistique · propriété intellectuelle. Détail : `docs/17-decisions/decisions-prealables.md`.
