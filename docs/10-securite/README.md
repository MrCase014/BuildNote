# K. Sécurité — À produire en Couche 6

> **Statut : À produire.** Dépend de la validation des Couches 1–4 et des décisions #1, #2, #4.

Contenu prévu :
- **Modèle de menaces** (STRIDE ou équivalent) pour chaque module et le socle.
- **Authentification** : comptes, MFA, politique de mots de passe, sessions, fédération éventuelle.
- **Autorisation** : RBAC + ABAC, rôles (enseignant, responsable, conseiller, chef d'établissement,
  admin SI, admin BuildNote, gestionnaire référentiel, élève, parent), principe du moindre privilège.
- **Séparation des établissements** (multi-tenant) : isolation par conception, tests d'isolation
  dédiés, clé établissement obligatoire, cloisonnement du stockage et des sauvegardes.
- **Chiffrement** : au repos (données, médias, secrets de connexion aux sources), en transit (TLS),
  gestion des clés.
- **Journalisation & audit** : traçabilité des accès et des actions sensibles (validation de notes,
  production de dossiers d'orientation, imports/exports, modifications du référentiel), lineage.
- **Sauvegardes & restauration** : politique, fréquence, tests de restauration, RPO/RTO, cas
  on-premise / cloud / hybride.
- **Confidentialité & protection des données** : minimisation, pseudonymisation pour l'analyse
  agrégée, consentement (Module 2), droits des personnes, DPIA finalisée, durées de conservation.
- **Contrôle d'accès physique et opérationnel** (selon hébergement).
- **Gestion des vulnérabilités** : mises à jour, revue de code sécurité, tests d'intrusion (Phase 9).
- **Conformité** : loi camerounaise N° 2010/012, socle type RGPD pour le multi-pays.

Risques liés : [`../16-risques/risques.md`](../16-risques/risques.md) R4, R10.
