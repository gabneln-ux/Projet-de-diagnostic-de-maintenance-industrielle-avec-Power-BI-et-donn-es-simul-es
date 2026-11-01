# DIAG-LINE — Plan de simulation industrielle

## 1. Objectif

Construire un jeu de données industriel synthétique pour analyser la performance de production, la fiabilité, la maintenance, la qualité et les possibilités d'amélioration technico-économique d'une ligne d'embouteillage.

Toutes les données générées sont fictives. Les résultats sont des résultats d'analyse du scénario simulé, et non des performances observées dans une usine réelle.

## 2. Configuration de référence

- Produit : boisson non gazeuse.
- Contenant : bouteille en PET.
- Remplissage : dosage volumétrique.
- Fermeture : bouchon à vis en plastique.
- Convoyage : chaîne modulaire motorisée.
- Conditionnement : étiquetage automatique puis regroupement sous film.
- Cadence nominale de référence : 6 000 bouteilles par heure.
- Période : du 1er juillet au 30 septembre 2026 inclus.
- Calendrier : production du lundi au samedi, dimanche sans production.
- Équipes : deux équipes par jour.
- Durée d'une équipe : 8 heures, dont 30 minutes de pause.
- Temps net planifié : 15 heures par jour.
- Production théorique de référence : 90 000 bouteilles par jour.
- Nombre de jours de production : 79.
- Temps net planifié sur la période : 1 185 heures.
- Production théorique de référence sur la période : 7 110 000 bouteilles.

La cadence de 6 000 bouteilles par heure est une hypothèse de conception. Elle devra être considérée comme la cadence nominale de la ligne uniquement si les capacités supposées des différents postes sont compatibles.

## 3. Périmètre des équipements

### M01 — Dépalettiseur
Fonction : transférer les bouteilles vides depuis les palettes vers la ligne.
Modes de défaillance simulables : défaut de positionnement, défaut de capteur, problème de préhension, blocage mécanique.

### M02 — Rinceuse
Fonction : rincer les bouteilles avant remplissage.
Modes de défaillance simulables : obstruction de buse, débit ou pression insuffisants, défaut de transfert, défaut de capteur.

### M03 — Remplisseuse
Fonction : doser la boisson dans les bouteilles.
Technologie de référence : dosage volumétrique.
Modes de défaillance simulables : dérive de dosage, vanne défectueuse, obstruction, défaut de synchronisation.

### M04 — Boucheuse
Fonction : poser et serrer les bouchons à vis.
Modes de défaillance simulables : alimentation irrégulière en bouchons, usure de tête, mauvais réglage de couple, défaut de synchronisation.

### M05 — Convoyeur motorisé
Fonction : transférer les bouteilles entre les postes.
Technologie de référence : chaîne modulaire entraînée par moteur électrique et réducteur.
Modes de défaillance simulables : désalignement, tension inadéquate, usure de roulement, défaut de transmission, surcharge ou bourrage.

### M06 — Étiquetage et conditionnement
Fonction : appliquer les étiquettes puis regrouper les bouteilles sous film.
Modes de défaillance simulables : défaut de détection, décalage d'étiquette, problème d'alimentation, bourrage du module de regroupement.

Ces modes sont des hypothèses plausibles de simulation et non des défauts réellement constatés.

## 4. Logique générale de la simulation

1. Générer le calendrier de production et les deux équipes des jours ouvrés.
2. Définir les ordres de production et les quantités théoriques.
3. Générer les événements d'arrêt avec début, fin, équipement, symptôme et impact estimé.
4. Relier les alarmes aux événements correspondants lorsqu'une alarme est pertinente.
5. Générer les interventions de maintenance associées à certains arrêts.
6. Générer les contrôles qualité et les quantités rejetées.
7. Générer les mesures de condition selon un calendrier explicite.
8. Générer les relevés énergétiques et les données de stock.
9. Proposer des actions d'amélioration dont les coûts et gains sont explicitement estimés.
10. Vérifier automatiquement les règles de cohérence avant d'utiliser les données.

La graine aléatoire sera fixe afin de reproduire le même jeu de données à chaque exécution.

## 5. Fréquences de référence proposées

- Production : une ligne par équipe et par jour de production.
- Arrêts : un enregistrement par événement.
- Maintenance : un enregistrement par intervention.
- Qualité : contrôles échantillonnés à des moments définis de la production.
- Mesures de condition : relevés périodiques simulés, par exemple toutes les deux heures de fonctionnement, complétés par des inspections planifiées si nécessaire.
- Alarmes : un enregistrement par événement pertinent, avec lien vers un arrêt lorsque cela s'applique.
- Inspections : un enregistrement par contrôle.
- Énergie : relevés horaires ou par période de fonctionnement, selon le modèle retenu.
- Stocks : état de référence des pièces et paramètres de réapprovisionnement.
- Actions : une ligne par proposition d'amélioration.

Ces fréquences sont des paramètres du scénario. Elles ne prétendent pas représenter l'instrumentation réelle d'une installation particulière.

## 6. Relations entre les données

- Un équipement peut être associé à plusieurs arrêts.
- Un arrêt peut être associé à zéro, une ou plusieurs alarmes.
- Un arrêt peut entraîner une intervention de maintenance.
- Une intervention peut concerner plusieurs opérations, mais chaque intervention doit posséder un identifiant unique.
- Un ordre de production peut être associé à plusieurs contrôles qualité.
- Les mesures de condition et les inspections doivent référencer un équipement existant.
- Les actions d'amélioration peuvent cibler un équipement ou un problème transversal.
- Les horodatages doivent permettre de reconstituer la séquence des événements.

## 7. Règles de cohérence

- Les identifiants doivent être uniques dans leur table.
- Les équipements référencés doivent exister.
- La date de fin d'un arrêt doit être postérieure à sa date de début.
- La durée d'un arrêt doit correspondre aux horodatages, selon la convention retenue.
- La production conforme ne peut pas dépasser la production totale.
- Les quantités rejetées ne peuvent pas dépasser les quantités contrôlées.
- Les coûts et durées doivent être non négatifs.
- Les unités doivent être explicites et homogènes.
- Les arrêts qui se chevauchent ne doivent pas être additionnés automatiquement comme des pertes de ligne indépendantes.
- Les pertes de production doivent tenir compte des éventuels arrêts simultanés et des capacités tampons.
- Les causes déclarées, les causes suspectées et les causes confirmées doivent rester distinctes.
- Une corrélation entre une mesure et une panne ne prouve pas à elle seule une causalité.
- Les valeurs manquantes doivent être signalées et non remplacées arbitrairement.

## 8. Criticité et analyse

Aucun équipement ne sera désigné comme le plus critique avant l'analyse.

La priorisation s'appuiera notamment sur :
- le nombre d'arrêts ;
- le temps d'arrêt et l'impact réel sur la ligne ;
- les pertes de production et les rebuts ;
- le MTBF et le MTTR lorsque les données le permettent ;
- les coûts de maintenance ;
- les conséquences possibles sur la sécurité, la qualité et l'environnement ;
- la disponibilité des pièces de rechange.

## 9. Évaluation économique

Les coûts de maintenance et les coûts de pièces seront identifiés séparément lorsque possible.

Les gains des actions d'amélioration seront estimés à partir d'hypothèses explicites. Ils ne seront pas présentés comme des économies réellement réalisées.

Toute comparaison avant/après sera identifiée comme une simulation de scénario tant qu'elle n'aura pas été validée par des données réelles.

## 10. Traçabilité et reproductibilité

- Documenter les paramètres de simulation.
- Fixer la graine aléatoire.
- Séparer les données brutes simulées des données transformées.
- Conserver les scripts de génération et de contrôle.
- Produire un rapport de validation des données.
- Documenter les limites du modèle et les hypothèses non vérifiées.

## 11. Capacités théoriques des équipements

Les capacités ci-dessous sont des hypothèses de simulation destinées à vérifier la cohérence du scénario. Elles ne représentent pas des spécifications constructeur.

| ID | Equipement | Capacite theorique (bouteilles/h) |
|---|---|---:|
| M01 | Depalettiseur | 7500 |
| M02 | Rinceuse | 8000 |
| M03 | Remplisseuse | 7000 |
| M04 | Boucheuse | 7000 |
| M05 | Convoyeur motorise | 7500 |
| M06 | Etiquetage et conditionnement | 6500 |

La cadence nominale cible de la ligne est fixee a 6000 bouteilles/h pour le scenario simule. La capacite theorique minimale retenue est de 6500 bouteilles/h, soit une marge de 8,3 % par rapport a la cadence cible.

Cette marge ne garantit pas la cadence effective. Les pertes de vitesse, les micro-arrets, les changements de format, les defauts qualite, les accumulations et les contraintes de synchronisation seront modelises separement lorsque necessaire.

Les capacites des differents postes devront etre exprimees dans une unite comparable. Pour M06, la cadence est exprimee en bouteilles traitees par heure, et non en paquets par heure.

Aucune capacite ne sera presentee comme une donnee constructeur ou une mesure reelle.

## 12. Modes de defaillance et hypotheses de simulation

Les modes ci-dessous sont des hypotheses de modelisation, et non des pannes observees sur une installation reelle. Les frequences sont exprimees en evenements pour 1000 heures de fonctionnement de l'equipement. Les durees sont des plages indicatives de duree d'indisponibilite par evenement.

| Equipement | Mode de defaillance simule | Frequence min (/1000 h) | Frequence max (/1000 h) | Duree min (min) | Duree max (min) |
|---|---|---:|---:|---:|---:|
| M01 | Blocage de palettes | 2 | 6 | 5 | 25 |
| M01 | Defaut de capteur | 1 | 4 | 5 | 20 |
| M01 | Defaut de prise ou de transfert | 1 | 3 | 15 | 45 |
| M02 | Buse obstruee | 2 | 6 | 5 | 25 |
| M02 | Defaut de pompe ou pression insuffisante | 1 | 3 | 15 | 60 |
| M02 | Defaut de capteur | 1 | 4 | 5 | 20 |
| M03 | Derive de dosage ou de remplissage | 2 | 5 | 10 | 35 |
| M03 | Defaut de vanne ou de joint | 1 | 3 | 20 | 90 |
| M03 | Bourrage ou defaut de transfert | 1 | 4 | 5 | 30 |
| M04 | Mauvais positionnement du bouchon | 2 | 6 | 5 | 30 |
| M04 | Usure de la tete de bouchage | 1 | 3 | 20 | 75 |
| M04 | Defaut d'alimentation en bouchons | 1 | 4 | 5 | 25 |
| M05 | Accumulation ou blocage de convoyage | 2 | 7 | 5 | 30 |
| M05 | Usure ou defaut de transmission | 1 | 3 | 20 | 90 |
| M05 | Defaut de detection ou de synchronisation | 1 | 4 | 5 | 25 |
| M06 | Defaut d'etiquetage | 2 | 6 | 5 | 30 |
| M06 | Bourrage du conditionnement sous film | 1 | 4 | 10 | 45 |
| M06 | Defaut de capteur ou de reglage | 1 | 4 | 5 | 25 |

### Regles d'utilisation

- Les plages servent de parametres initiaux au generateur de donnees. Elles pourront etre ajustées apres les premiers controles de coherence.
- Les evenements seront tires de maniere reproductible avec une graine aleatoire documentee.
- Les frequences seront appliquees au temps de fonctionnement simule, et non automatiquement au nombre de jours calendaires.
- La duree d'une panne sera distinguee de son impact sur la ligne : un equipement peut etre arrete sans provoquer une perte de production equivalente si un tampon ou une accumulation absorbe l'incident.
- Les arrets simultanes ou lies entre equipements ne devront pas etre additionnes aveuglement pour calculer la perte totale de la ligne.
- Les symptomes, causes declarees et causes confirmees seront stockes distinctement. Une cause simulee ne sera jamais presentee comme une conclusion de diagnostic reel.
- Aucun equipement n'est designe a l'avance comme le plus critique. Le classement sera etabli apres generation et analyse des donnees.


## 13. Logique de generation des evenements et des arrets

### 13.1 Base temporelle
- La periode comprend 79 jours de production et 1185 heures planifiees nettes pour la ligne.
- Le calendrier de production sera genere en premier, avec deux equipes par jour et les pauses planifiees exclues du temps net.
- Les evenements ne seront places que dans les plages de production planifiees.
- Pour chaque equipement, le generateur conservera le temps planifie, le temps d'arret simule et le temps de fonctionnement estime.
- Les frequences de defaillance seront parametrees par 1000 heures de fonctionnement. Le calcul initial utilisera une estimation du temps d'exposition; les frequences obtenues seront ensuite recalculees sur le temps de fonctionnement estime et controlees pour coherence.

### 13.2 Creation des evenements
- Chaque evenement recevra un identifiant unique, un equipement, un mode de defaillance, un debut, une fin, une duree et un symptome.
- La duree sera tiree dans la plage associee au mode de defaillance.
- Les evenements seront limites aux plages de production et ne pourront pas avoir une duree negative ou nulle.
- Une graine aleatoire fixe sera utilisee afin de reproduire les memes donnees lors d'une nouvelle execution avec les memes parametres.
- Les arrets qui depassent la fin d'une plage de production seront tronques a cette limite ou reprogrammes selon une regle documentee; ils ne seront jamais prolonges silencieusement hors calendrier.

### 13.3 Effet sur la ligne
- Un arret d'equipement et une perte de production de la ligne sont deux mesures distinctes.
- Les equipements seront relies par leur ordre fonctionnel : depalettiseur, rinceuse, remplisseuse, boucheuse, convoyeur et etiquetage-conditionnement.
- Le generateur distinguera les arrets locaux, les arrets susceptibles de bloquer la ligne et les incidents absorbes par un tampon.
- En l'absence de modele detaille des tampons, l'impact sur la ligne sera une estimation simulee, identifiee comme telle.
- Les chevauchements temporels entre incidents seront conserves. La perte totale de ligne sera calculee sur les intervalles d'indisponibilite de la ligne, sans additionner plusieurs fois le meme intervalle.

### 13.4 Production et qualite
- La production theorique sera calculee a partir du temps planifie et de la cadence nominale de 6000 bouteilles/h.
- La production totale sera limitee par la capacite theorique de la ligne et ajustee par les pertes simulees.
- La production conforme ne pourra pas depasser la production totale.
- Les rebuts seront non negatifs et ne pourront pas depasser la production totale.
- Les defauts qualite pourront etre associes a certains modes de defaillance, sans supposer qu'une panne entraine systematiquement un defaut.

### 13.5 Validation
- Verifier l'unicite des identifiants et l'integrite des relations entre fichiers.
- Verifier les dates, durees, unites, limites de production et valeurs numeriques.
- Verifier qu'aucun evenement n'est place le dimanche ou pendant une pause planifiee.
- Produire un rapport indiquant les controles reussis, les anomalies detectees et les corrections appliquees.
- Toutes les donnees produites restent fictives et devront etre identifiees comme simulees dans les analyses et le portfolio.
