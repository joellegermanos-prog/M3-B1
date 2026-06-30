# Note d'identification des sources — Acerox Métallurgie

> Document remis à **Sébastien Marchand** (chef de projet industrialisation
> Acerox). **2-3 pages max.** Public : décideur métier non-technique —
> langage courant, pas de jargon scikit-learn ou SQL.
> Auteur : `<prénom>` — Date : `<date>`

## 1. Contexte

> 1 paragraphe — qui est Acerox ? quel est leur existant ? quelle est la
> demande FastIA ?

Acerox Métallurgie est un acteur industriel disposant de plusieurs sites de production et d’un modèle existant de prédiction des défauts qualité. L’objectif de la mission est d’identifier de nouvelles sources de données susceptibles d’enrichir ce modèle. FastIA intervient pour cadrer le besoin métier, analyser les données disponibles.

## 2. Demande métier reformulée

> 1 paragraphe — ce que Sébastien veut **vraiment**, distingué de ce qu'il
> a *dit*. Reformulation en termes de décision métier à améliorer.

Ce que Sébastien a demandé : Enrichir le modèle existant avec de nouvelles données pour anticiper les défauts qualité au moins 24h avant la production

Ce que je comprends qu'il cherche vraiment : Améliorer la prise de décision en amont de la production en identifiant les situations à risque suffisamment tôt pour ajuster les paramètres de fabrication, planifier des actions préventives et réduire les défauts. L’objectif est d’optimiser la qualité de production et de diminuer les rebuts, notamment sur des lignes sensibles comme celle de Roubaix.

## 3. Inventaire des sources

> Une ligne par source que **vous** avez identifiée (fichiers reçus +
> ce que vous découvrez en explorant les données). Le nom exact du fichier
> fait partie de l'inventaire à dresser.


| Source | Format | Volume | Fréquence | Qualité observée | Risques RGPD | Pertinence métier |
|---|---|---|---|---|---|---|
| `capteurs_iot.csv` | CSV  | 51 000 lignes × 7 colonnes (~3,5 MB) | continue (1 mois échantillonné) | ~1,47 % de valeurs manquantes sur `vibration_mms` | Faible (pas de données personnelles) | Haute  — mesures directes des conditions de production (température, vibration, débit) utiles pour détecter les défauts |
| `erp_export.json` | JSON | 2 000 lignes × 9 colonnes (~546 KB) | Batch (export ERP périodique) | Structure cohérente ; ~5,45 % de valeurs manquantes sur `ouvrier_id` ; dates en texte à convertir | Moyen — `ouvrier_id` pseudonymisé, risque de réidentification par croisement avec logs, planning ou données IoT | Haute — contexte des ordres de production (produit, ligne, dates) essentiel pour anticiper les défauts |
| `logs_machines.log` | Texte semi-structuré | 30 000 lignes (~1,8 MB) | Continue (logs machines) | Format régulier mais non structuré ; parsing nécessaire ; événements INFO/WARN/ERROR exploitables ; messages techniques pertinents | Moyen — événements type `operator_login`, `shift_changed` peuvent permettre une réidentification indirecte via croisement | Moyenne — utile pour expliquer et confirmer les anomalies détectées par les capteurs |

## 4. Recommandations

> 3-5 puces. Quelles sources ingérer en priorité ? Lesquelles écarter et
> pourquoi ?


- **Prioriser l’ingestion des capteurs IoT** :  
  source clé pour capturer les conditions physiques de production (température, vibration, débit) et détecter les signaux faibles annonciateurs de défauts.

- **Intégrer en priorité les données ERP** :  
  indispensables pour contextualiser les données techniques (produit, ligne, dates) et permettre une analyse orientée métier, notamment pour anticiper les défauts avant production.

- **Intégrer les logs machines en complément** :  
  utiles pour expliquer et confirmer les anomalies détectées (ex. vibration_overlimit), mais nécessitant un effort de parsing et de structuration préalable.

- **Encadrer les données sensibles (RGPD)** :  
  pseudonymiser ou supprimer le champ `ouvrier_id` et limiter l’usage des événements opérateurs afin de réduire les risques de réidentification par croisement.

- **Mettre en place un alignement temporel des données** :  
  synchroniser IoT, ERP et logs autour du timestamp pour garantir une exploitation cohérente et répondre à l’objectif d’anticipatio


## 5. Points à clarifier avec Sébastien

> 3-5 questions ouvertes restantes — preuve de lucidité sur ce qu'on ne
> sait pas encore.

1. ...
2. ...
3. ...

## 6. Limites de cette note

> Ce qu'on n'a **pas** fait, et qu'il faudrait faire plus tard.

- Pas d'analyse statistique fouillée des sources (M3-B1 = identification,
  pas EDA complète)
- Pas d'AIPD juridique formelle (recommandation : escalader au DPO Acerox)
- Pas de conception ni d’évaluation du modèle existant (hors périmètre, modèle déjà en place chez Acerox).
- Pas de mise en œuvre technique (ingestion, pipeline, BDD)

---

*Note produite par <prénom>, <date>, dans le cadre du brief M3-B1 ATOS.*
