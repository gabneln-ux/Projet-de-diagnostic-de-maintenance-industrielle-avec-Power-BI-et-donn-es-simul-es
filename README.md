# DIAG-LINE — Diagnostic de maintenance industrielle

## Présentation

DIAG-LINE est un projet de portfolio d'ingénierie électromécanique et de data industrielle. Il utilise Power BI et des scripts Python pour explorer des données simulées de maintenance d'une ligne de conditionnement.

## Problématique

Quels équipements et quelles défaillances méritent une attention prioritaire, et quelles actions peut-on proposer à partir des données disponibles ?

## Objectifs

- Analyser les arrêts et leur répartition par équipement.
- Explorer les alarmes et les mesures de condition.
- Examiner les coûts de maintenance.
- Hiérarchiser les équipements et les actions proposées.
- Présenter les résultats dans un tableau de bord Power BI.

## Outils

- Power BI
- Python
- Pandas
- CSV
- PowerShell pour certaines opérations de préparation du projet

## Rapport Power BI

Le fichier `powerbi/deee.pbix` contient le rapport interactif.

## Données et limites

Toutes les données sont simulées à des fins de démonstration. Les résultats ne proviennent pas d'une installation industrielle réelle.

Les causes de défaillance sont des éléments d'analyse et ne doivent pas être considérées comme des causes racines confirmées sur le terrain. Les coûts, budgets et gains associés aux actions sont estimatifs ou hypothétiques.

Les résultats doivent être validés par des observations terrain avant toute décision industrielle réelle.

## Structure du dépôt

- `data/` : jeux de données du projet.
- `docs/` : dictionnaire des données, hypothèses et règles de cohérence.
- `images/` : captures du rapport, à ajouter.
- `powerbi/` : rapport Power BI.
- `python/` : scripts de génération, préparation et audit des données.

## Reproduction

Les scripts peuvent dépendre de chemins locaux, de fichiers intermédiaires ou d'une base SQLite. Leur ordre d'exécution et leurs prérequis doivent être vérifiés avant de tenter une reproduction complète depuis un autre ordinateur.

## Auteur

Projet de portfolio — ingénierie électromécanique, maintenance industrielle et analyse de données.
