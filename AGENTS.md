# BuildNote — Référence projet pour les assistants IA

> Ce fichier est la **carte du projet**. Tout modèle (Claude Code, agents, autres LLM) doit le lire
> **avant toute modification** et s'y référer pour savoir *où* écrire, *dans quelle langue*, *à quelle
> couche* et *ce qui est interdit à ce stade*.
> `CLAUDE.md` et `AGENTS.md` ont un contenu identique — mettre à jour les deux ensemble.

---

## 1. Nature du projet

**BuildNote** = plateforme d'aide à la décision éducative (initiative **privée**, ambition
multi-établissements, **Cameroun**, extensible multi-pays). Deux modules **fonctionnellement
séparés**, ne partageant que le socle commun et communiquant par contrats d'API explicites :

| | Module 1 — Capture & gestion des données académiques | Module 2 — Orientation scolaire & universitaire |
|---|---|---|
| **But** | Transformer une fiche physique en données structurées **vérifiées** | Éclairer l'orientation + lire la performance (dashboard) |
| **Cœur** | OCR / Computer Vision / Document Understanding + **validation humaine obligatoire** | Moteur de règles + scoring multi-critères pondéré + génération d'**explications** |
| **Couplage** | Écrit dans la base normalisée (après validation) | Lit la base normalisée + le référentiel stratégique national, **à la demande** |

**Règles produit non négociables :**
1. Le Module 2 **ne recalcule rien automatiquement** ; dashboard et orientation lisent les bases **à la demande**.
2. Le Module 1 n'enregistre **jamais** une sortie OCR sans **revue humaine**.
3. Les recommandations d'orientation sont **explicables** et restent une **aide à la décision** — aucune carrière imposée.

Contexte de conception : SI scolaires hétérogènes ou inexistants, connectivité faible
(**offline-first** pour le Module 1), matériel modeste, interface **bilingue FR/EN**, architecture
**modulaire, interopérable, multi-tenant**.

---

## 2. Règles de travail (état au 2026-09-08)

- **Aucun code** tant que cadrage → conception → POC ne sont pas validés. Le code démarre en
  **Phase 8**, après le Go/No-Go de la **Phase 7**. Les phases 0→6 sont **sans code**.
- Toute la production vit dans **`docs/`** : **Markdown + diagrammes Mermaid**, **en français**
  (le produit reste bilingue FR/EN).
- Production **par couches**, avec une **porte de validation** entre chacune. Ne pas produire une
  couche N+1 tant que la couche N n'est pas validée.
- **Pas de MVP** (choix du porteur) → recommandation actée : **déploiement pilote progressif**.
- Chaque document porte un en-tête `> **Statut : …**` (Brouillon / En revue / Validé / À produire /
  Vivant) et une **date**.
- Les décisions d'architecture se tracent en **ADR** dans `docs/17-decisions/`.
- Terminologie imposée : `docs/glossaire.md` (FR + équivalent EN). Réutiliser ces termes exactement.
- Dates : **absolues** (jamais « la semaine prochaine »).

---

## 3. Structure du dépôt

```
BuildNote/
├── CLAUDE.md                     # ce fichier (référence projet)
├── AGENTS.md                     # copie identique de CLAUDE.md
├── images/                       # logos (logo.jpeg, logo1..4.jpeg) — actifs de marque
└── docs/                         # corpus documentaire d'ingénierie (Markdown + Mermaid)
    ├── README.md                 # PORTE D'ENTRÉE : table des couches + synthèse exécutive (10 points) — suivi d'avancement
    ├── glossaire.md              # [Vivant] terminologie FR/EN imposée
    │
    ├── 00-vision/
    │   └── vision-produit.md     # [Couche 1] A. Vision produit
    ├── 01-project-management/
    │   ├── roadmap.md            # [Couche 1] B. Phases 0→11, jalons J0→J11, portes go/no-go
    │   ├── project-charter.md    # [Couche 2] B.1 document fondateur
    │   ├── gouvernance.md        # [Couche 2] B.2 principes, RACI
    │   ├── methodologie.md       # [Couche 2] B.3 hybride à portes de décision
    │   └── gestion-changements-versions-documentaire.md  # [Couche 2] B.4
    ├── 02-analyse-metier/
    │   ├── README.md             # sommaire de la section
    │   ├── analyse-metier.md     # [Couche 2] C. problématique, besoins, AS-IS/TO-BE
    │   ├── personas.md           # [Couche 2] C. personas & parcours utilisateurs
    │   └── cas-usage.md          # [Couche 2] C. cas d'utilisation
    ├── 03-cahier-des-charges/
    │   ├── README.md             # sommaire de la section
    │   ├── exigences-fonctionnelles.md        # [Couche 3] D. exigences F
    │   ├── exigences-non-fonctionnelles.md    # [Couche 3] D. exigences NF
    │   └── contraintes-kpi-tracabilite.md     # [Couche 3] D. contraintes, critères d'acceptation, KPI, matrice de traçabilité
    ├── 04-architecture-fonctionnelle/
    │   └── architecture-fonctionnelle.md  # [Couche 1] E. les 2 modules, séparés
    ├── 05-architecture-technique/
    │   ├── README.md             # sommaire de la section
    │   └── scenarios-architecture.md  # [Couche 3/4] F. scénarios d'architecture comparés + choix
    ├── 06-architecture-donnees/
    │   ├── vue-ensemble.md       # [Couche 1] G. strates Raw / Normalized / Intelligence
    │   └── modele-conceptuel-logique-physique.md  # [Couche 4] G. MCD / MLD / MPD + dictionnaire de données
    ├── 07-interoperabilite/
    │   ├── vue-ensemble.md       # [Couche 1] H. modèle canonique, connecteurs, mapping, ETL
    │   └── architecture-detaillee.md  # [Couche 4] H. catalogue connecteurs, langage de mapping, conflits, lineage, versioning schéma, qualité
    ├── 08-ocr-computer-vision/
    │   └── README.md             # [À produire — Couche 5] I. pipeline capture → validation humaine → stockage
    ├── 09-moteur-orientation/
    │   └── vue-ensemble.md       # [Couche 1] J. fusion multi-sources + explicabilité + dimension nationale (détail → Couche 5)
    ├── 10-securite/
    │   └── README.md             # [À produire — Couche 6] K. authn/authz, chiffrement, audit, isolation multi-tenant
    ├── 11-ux-ui/
    │   └── README.md             # [À produire — Couche 6] L. UX, design system (bleu clair / orange / blanc), i18n FR/EN
    ├── 12-poc/
    │   └── README.md             # [À produire — Couche 7] M. POC OCR, extraction tableaux, interop, moteur d'orientation (jetables)
    ├── 13-tests/
    │   └── README.md             # [À produire — Couche 7] O. stratégie et plans de test
    ├── 14-deploiement/
    │   └── README.md             # [À produire — Couche 7] P. 6 scénarios de déploiement
    ├── 15-livrables-par-phase/
    │   └── livrables.md          # [Couche 1] Q. par phase : objectif/activités/livrables/critères/responsables/dépendances/go-no-go
    ├── 16-risques/
    │   └── risques.md            # [Vivant] registre R1→R12 + mitigations, revu à chaque jalon
    └── 17-decisions/
        └── decisions-prealables.md  # [Vivant] 12 décisions à arbitrer en Phase 2 + ADR
```

### Correspondance couches ↔ phases

| Couche | Contenu | Phase(s) du cycle de vie |
|---|---|---|
| **1** (livrée le 2026-09-08, à valider) | Vision, archi fonctionnelle, vues d'ensemble données/interop/orientation, roadmap, livrables, risques, décisions, glossaire | 0 |
| **2** | Project management complet, analyse métier, personas, cas d'usage | 0–1 |
| **3** | Cahier des charges, architecture technique | 2–3 |
| **4** | Architecture données détaillée (MCD/MLD/MPD), interopérabilité détaillée, sécurité | 4 |
| **5** | OCR/CV détaillé, moteur d'orientation détaillé | 4–5 |
| **6** | Sécurité, UX/UI | 4–6 |
| **7** | POC, tests, déploiement, consolidation des livrables | 6–7 |

> Les fichiers `README.md` marqués **« À produire »** sont des **stubs** : ils décrivent le contenu
> attendu de la section et sa couche. Ne pas les étoffer avant que leur couche soit ouverte.

---

## 4. Où intervenir selon la demande

| La demande porte sur… | Fichier(s) à modifier |
|---|---|
| Vision, finalités, cibles | `docs/00-vision/vision-produit.md` |
| Phases, jalons, planning, portes | `docs/01-project-management/roadmap.md` (+ autres fichiers `01-*` si Couche 2) |
| Séparation des modules, contrats, flux fonctionnels | `docs/04-architecture-fonctionnelle/architecture-fonctionnelle.md` |
| Exigences F / NF, contraintes, critères d'acceptation, KPI | `docs/03-cahier-des-charges/exigences-fonctionnelles.md`, `exigences-non-fonctionnelles.md`, `contraintes-kpi-tracabilite.md` |
| Scénarios d'architecture technique, choix de stack | `docs/05-architecture-technique/scenarios-architecture.md` |
| Strates de données, modèle canonique | `docs/06-architecture-donnees/vue-ensemble.md` ; MCD/MLD/MPD → `modele-conceptuel-logique-physique.md` |
| Connecteurs, mapping, ETL, qualité des données | `docs/07-interoperabilite/vue-ensemble.md` ; détail → `architecture-detaillee.md` |
| Pipeline OCR / vérification humaine | `docs/09-moteur-orientation/vue-ensemble.md` (moteur) / `docs/08-ocr-computer-vision/README.md` (pipeline) |
| Explicabilité, scoring, référentiel national | `docs/09-moteur-orientation/vue-ensemble.md` |
| Un risque nouveau ou modifié | `docs/16-risques/risques.md` |
| Une décision structurante | `docs/17-decisions/decisions-prealables.md` (option + recommandation) ou nouvel **ADR** |
| Un terme métier/technique | `docs/glossaire.md` |
| Livrables / critères de validation d'une phase | `docs/15-livrables-par-phase/livrables.md` |
| Suivi d'avancement, table des couches | `docs/README.md` |

**Après toute modification de structure** (nouveau dossier/fichier, changement de couche, de statut) :
mettre à jour la table de `docs/README.md` **et** l'arborescence de la section 3 ci-dessus (dans
`CLAUDE.md` et `AGENTS.md`).

---

## 5. Checklist avant d'écrire

- [ ] La demande relève-t-elle d'une couche **déjà ouverte** ? Sinon, le signaler et ne pas produire.
- [ ] Est-ce du **code** ? Si oui → refuser à ce stade (phases 0–6 sans code) et proposer l'équivalent documentaire.
- [ ] Rédaction **en français**, format **Markdown**, diagrammes en **Mermaid**.
- [ ] En-tête `Statut` + date présent et cohérent.
- [ ] Termes conformes au **glossaire** ; enrichir le glossaire si un terme manque.
- [ ] Liens internes relatifs corrects (`../dossier/fichier.md`).
- [ ] Répercuter dans `docs/README.md` (table des couches / suivi) et dans l'arborescence de ce fichier si la structure change.
- [ ] Cohérence avec les **3 règles produit non négociables** (§1) et les décisions déjà arbitrées.
