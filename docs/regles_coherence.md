# DIAG-LINE — Règles de cohérence et relations

## Identifiants
- equipement_id référence le référentiel des équipements.
- arret_id identifie un arrêt unique.
- intervention_id identifie une intervention unique.
- ordre_production_id identifie un ordre de fabrication.
- piece_id identifie une pièce de rechange.
- action_id identifie une action d'amélioration.

## Relations
- Un équipement peut être associé à plusieurs arrêts.
- Un arrêt peut être associé à zéro, une ou plusieurs alarmes.
- Un arrêt peut déclencher une intervention de maintenance.
- Une intervention peut utiliser plusieurs pièces.
- Un ordre de fabrication peut avoir plusieurs contrôles qualité.
- Les mesures techniques sont horodatées et rattachées à un équipement.
- Une action d'amélioration peut cibler un équipement ou un problème transversal.

## Contrôles de cohérence
- La date de fin d'un arrêt doit être postérieure à sa date de début.
- La durée calculée doit être cohérente avec les horodatages.
- La production conforme ne peut pas dépasser la production totale.
- Les rebuts ne peuvent pas dépasser la quantité produite.
- Les références d'équipement et de pièce doivent exister.
- Les unités doivent être explicites et homogènes.
- Les coûts estimés doivent être non négatifs.
- Les valeurs manquantes doivent être identifiées, pas remplacées arbitrairement.

## Rigueur analytique
- Les données sont fictives et simulées.
- Symptôme, cause déclarée et cause confirmée sont des notions distinctes.
- Les relations statistiques ne prouvent pas à elles seules une causalité.
- Les gains d'amélioration sont des estimations à valider sur le terrain.
