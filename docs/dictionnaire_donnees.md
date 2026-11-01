# DIAG-LINE — Dictionnaire des données

## 1. Production — production_journaliere.csv
- date : date de production.
- equipe : équipe de production.
- ordre_production_id : identifiant de l'ordre.
- produit_id : référence du produit.
- temps_planifie_h : temps planifié en heures.
- production_theorique : quantité théorique en bouteilles.
- production_totale : quantité produite.
- production_conforme : quantité conforme.
- rebuts : quantité rejetée.
- cadence_moyenne_bph : cadence moyenne en bouteilles par heure.

## 2. Arrêts — arrets.csv
- arret_id : identifiant unique de l'arrêt.
- debut : date et heure de début.
- fin : date et heure de fin.
- equipement_id : équipement concerné.
- categorie : planifié ou non planifié.
- symptome : symptôme observé.
- cause_declaree : cause déclarée ou suspectée.
- duree_min : durée de l'arrêt en minutes.
- impact_production : estimation des bouteilles perdues ; valeur ? calculer ou ? justifier.
- statut_donnee : indique le statut simul? de la donn?e.

## 3. Qualité — qualite.csv
- controle_id : identifiant du contrôle.
- date_heure : date et heure du contrôle.
- ordre_production_id : ordre concerné.
- equipement_id : équipement associé si connu.
- type_defaut : nature du défaut.
- quantite_controlee : quantité inspectée.
- quantite_rejetee : quantité rejetée.
- gravite : niveau de gravité.

## 4. Maintenance — maintenance.csv
- intervention_id : identifiant de l'intervention.
- equipement_id : équipement concerné.
- arret_id : arrêt associé si applicable.
- date_debut : début de l'intervention.
- date_fin : fin de l'intervention.
- type_maintenance : corrective, préventive ou conditionnelle.
- symptome : problème observé.
- travail_effectue : action effectuée.
- piece_id : pièce utilisée si applicable.
- cout_main_oeuvre_fcfa : coût estimé de main-d'œuvre.
- cout_pieces_fcfa : coût estimé des pièces.

## 5. ?quipements ? equipements.csv
- equipement_id : identifiant unique de l'?quipement.
- nom : nom de l'?quipement.
- fonction : fonction dans la ligne de production.
- fabricant : fabricant fictif ou r?f?rence simul?e.
- puissance_kw : puissance nominale du moteur, inconnue ? ce stade.
- vitesse_nominale_rpm : vitesse nominale en tr/min, inconnue ? ce stade.
- criticite_initiale : criticit? initiale ? ?valuer, sans pr?sumer du r?sultat.
- date_mise_service : date de mise en service simul?e, inconnue ? ce stade.
- capacite_theorique_bph : capacit? th?orique simul?e en bouteilles par heure ; hypoth?se non valid?e par un constructeur.
- statut_donnee : statut de la donn?e, par exemple hypothese_simulee.

## 6. Mesures de condition — mesures_condition.csv
- mesure_id : identifiant de la mesure.
- date_heure : horodatage de la mesure.
- equipement_id : équipement mesuré.
- composant : composant inspecté.
- temperature_c : température en degrés Celsius.
- vibration_mm_s : vibration en mm/s RMS.
- courant_a : courant électrique en ampères.
- vitesse_rpm : vitesse mesurée en tr/min.
- statut_mesure : normal, alerte ou à vérifier selon les seuils retenus.

## 7. Alarmes — alarmes.csv
- alarme_id : identifiant de l'événement.
- date_heure : date et heure.
- equipement_id : équipement associé.
- code_alarme : code simulé.
- description : description de l'alarme.
- severite : niveau de sévérité.
- arret_id : arrêt associé si applicable.
- duree_s : durée de l'événement en secondes.

## 8. Inspections mécaniques — inspections.csv
- inspection_id : identifiant de l'inspection.
- date_heure : date et heure.
- equipement_id : équipement inspecté.
- composant : composant contrôlé.
- controle : contrôle effectué.
- mesure : valeur mesurée si applicable.
- unite : unité de mesure.
- resultat : conforme, anomalie ou à confirmer.
- recommandation : contrôle ou action recommandée.

## 9. Énergie — energie.csv
- mesure_energie_id : identifiant de la mesure.
- date_heure : date et heure.
- equipement_id : équipement mesuré.
- duree_fonctionnement_h : durée de fonctionnement.
- energie_kwh : énergie consommée en kWh.
- production_associee : quantité produite durant la période.
- cout_energie_fcfa : coût énergétique estimé.

## 10. Stocks de pièces — stocks_pieces.csv
- piece_id : identifiant de la pièce.
- designation : nom de la pièce.
- equipement_id : équipement compatible.
- quantite_stock : quantité disponible.
- seuil_minimum : seuil de réapprovisionnement.
- cout_unitaire_fcfa : coût unitaire estimé.
- delai_approvisionnement_j : délai fournisseur estimé.
- criticite : criticité de la pièce.

## 11. Actions d'amélioration — actions.csv
- action_id : identifiant de l'action.
- equipement_id : équipement ciblé.
- probleme_cible : problème traité.
- hypothese_cause : cause à vérifier.
- action_proposee : action recommandée.
- cout_estime_fcfa : coût estimé de mise en œuvre.
- gain_annuel_estime_fcfa : gain annuel potentiel estimé.
- priorite : priorité proposée.
- indicateur_suivi : KPI à surveiller.
- statut_validation : statut de validation de l'action.

## Règles de qualité des données
- Tous les identifiants doivent être cohérents entre les fichiers.
- Les dates et heures doivent respecter une chronologie plausible.
- Les durées et quantités ne doivent pas être négatives.
- Les données sont simulées et doivent être identifiées comme telles.
- Les causes suspectées ne sont pas des causes confirmées.
- Les gains financiers sont des estimations fondées sur des hypothèses explicites.
- Les mesures de condition doivent être interprétées selon le composant,
  les conditions de fonctionnement et les seuils de référence appropriés.
