# Notes d'entretien — Sébastien Marchand (Acerox)

> Notes prises au fil de l'eau pendant l'entretien fictif 9h30-10h00.
> **5 catégories à pré-remplir** avant l'entretien. Tu complètes au fil
> de l'eau. Distinction explicite *dit* (ce que Sébastien a effectivement
> formulé) vs *interprété* (ta lecture).
>
> Conservé en livrable du brief.

**Date** : `30/06/2026` — **Durée** : 30 min — **Présents** : Sébastien Marchand (chef de projet industrialisation Acerox) + `Joelle Germanos` (FastIA)

---

## 1. Besoin métier

> Quelle décision Sébastien veut-il améliorer ? Quel KPI métier ?

**Dit** : Anticiper les defaut au moin 24h avant la production
Taux d’anticipation des défauts

**Interprété** : Améliorer la capacité à détecter en amont les situations à risque afin d’ajuster la production. 

**Dit** : Pas de priorisation de type de défaut à détecter

**Interprété** pas de catégorisation des défauts nécessaire, mais ce qui compte c'est la prédiction d'un défaut quel qu'il soit.


## 2. Sources et formats

> Qu'a-t-il à disposition ? Où ? Sous quel format ?

**Dit** : fichier csv, texte brut

**Interprété** : Présence de plusieurs sources hétérogènes

## 3. Volumétrie et fréquence

> Combien de données ? À quelle cadence arrivent-elles ?

**Dit** : Données depuis 2 ans

**Interprété** : Volumetrie importante

**Dit** : 3 site de productions, centralisé à Lyon

**Interprété** : production continue (données centralisés)

## 4. Contraintes (RGPD, sécurité, propriété)

> Quelles obligations légales ? Qui possède les données ? Quels accès
> sécurisés ?

**Dit** : Données sont local, Souveraineté

**Interprété** : Les données sont hébergées en local, ce qui traduit une contrainte forte de souveraineté et probablement une volonté de limiter l’exposition à des infrastructures cloud externes.  

## 5. Critères de succès

> Comment Sébastien saura-t-il qu'on a réussi ?

**Dit** : Baisse de – 20% sur la ligne de roubais

**Interprété** : L’objectif principal est une amélioration mesurable de la performance industrielle, avec une réduction significative des défauts qualité sur une ligne critique (Roubaix). 

**Dit** : Fausse alerte peu couteux par rapport à une pièce non conforme, mais il ne faut pas qu'il y en ait fréquement

**Interprété** : Fausse alerte mieux qu'une absence de détection


---

## Questions restées sans réponse

> Notes-le honnêtement — c'est précieux pour la note d'identification.

- Contraintes IT, sécurité, et conformité
- Combien de données ? À quelle cadence arrivent-elles ?
- Combien de défauts sont actuellement détectés par le modèle existant ?
- Disposez-vous d’un historique de défauts labellisés ?

## Mes impressions à chaud (10 min après)

> 1 paragraphe, à toi.

Sébastien exprime un besoin métier centré sur la réduction des défauts qualité et leur anticipation en amont, mais avec une formulation encore floue sur les aspects data et techniques. L’enjeu principal sera de structurer cette demande en un cas d’usage exploitable, notamment en validant la disponibilité des données.

---

*Notes d'entretien produites par <Joelle>, <30/06/2026>.*
