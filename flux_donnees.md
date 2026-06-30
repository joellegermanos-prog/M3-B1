# Schéma des flux de données — Acerox Métallurgie

> Schéma Mermaid à compléter. Doit montrer :
> - **Sources** (capteurs IoT, ERP, logs, *bonus PDF*)
> - **Ingestion** (à concevoir en M3-B2)
> - **BDD pivot** (à modéliser en M3-B2)
> - **Modèle existant** Acerox (placeholder, hors-sujet ici)
>
> Légende explicite : qui produit, qui consomme, contraintes.

## Schéma

```mermaid
flowchart LR
    %% TODO — Compléter avec tes 3 sources retenues + 1 bonus si traité

    SRC1[📡 Capteurs IoT<br/>Format :CSV<br/>Volume : 51k lignes x 9 colonnes<br/>Fréquence : continue]
    SRC2[📋 ERP<br/>Format : JSON<br/>2 000 ordres<br/>]
    SRC3[📝 Logs machines<br/>Format : texte<br/>Volume : 30k lignes<br/>Fréquence : continue]

    INGEST[🔄 Ingestion<br/>à concevoir en M3-B2]
    BDD[(🗄️ BDD pivot<br/>SQLite)]
    MODEL[🧠 Modèle existant Acerox<br/>prédiction défauts qualité]

    SRC1 --> INGEST
    SRC2 --> INGEST
    SRC3 --> INGEST
    INGEST -->|normalisation + dédup| BDD
    BDD -->|consommée par| MODEL

    classDef source fill:#e1f5ff,stroke:#0277bd
    classDef tofix fill:#fff4e1,stroke:#c97a00,stroke-dasharray: 5 5
    class SRC1,SRC2,SRC3 source
    class INGEST tofix
```

## Légende

> Reformule en 5 lignes max ce que le schéma raconte (qui produit quelle
> donnée, qui consomme, contraintes critiques).

- **Producteur** : les capteurs IoT (mesures machines), l’ERP (ordres de fabrication) et les logs machines (événements techniques) produisent les données sources.
- **Consommateur final** :  le modèle existant Acerox, utilisé pour prédire les défauts qualité.
- **Contraintes critiques** (fréquence / RGPD / qualité) : vigilance sur `ouvrier_id` (ERP) et événements opérateurs (logs) car risque de réidentification par croisement.

## Décisions associées

- Source(s) retenues en priorité : 
  - `capteurs_iot.csv` : données techniques essentielles pour détecter les dérives machines.
  - `erp_export.json` : contexte des ordres de fabrication, indispensable pour relier défauts et production.

- Source(s) écartées : Aucune source écartée à ce stade.
- Source bonus (PDF) traitée ? oui / non, pourquoi : Non, pertinente uniquement pour de la recherche sémantique (RAG) en aide au diagnostic, pas pour la prédiction tabulaire.

---

*Schéma produit par <Joelle>, <30/06/2026>, dans le cadre du brief M3-B1 ATOS.*
