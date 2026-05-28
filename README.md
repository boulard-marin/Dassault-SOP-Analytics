# 🎯 DÉMO INTERACTIVE — Lancer la démo en un clic !

> 🚀 **Recruteur ? Testez les analyses S&OP en direct dans votre navigateur, sans installation.**

Cliquez sur le badge ci-dessous pour lancer le notebook Jupyter hébergé gratuitement sur Binder :

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/boulard-marin/Dassault-SOP-Analytics/main?filepath=notebooks/demo_dassault.ipynb)

**Ou lancez directement via Voilà (interface plus fluide)** :

[![Voilà](https://img.shields.io/badge/Voilà-Interactive%20Dashboard-blueviolet?style=flat-square&logo=jupyter)](https://mybinder.org/v2/gh/boulard-marin/Dassault-SOP-Analytics/main?urlpath=voila/tree/notebooks/demo_dassault.ipynb)

**Temps de chargement** : 30-60 secondes (première visite) — **Aucune installation requise** ✨

### 📊 Que verrez-vous ?

La démo interactive comprend :

- 📈 **Graphiques Plotly interactifs** : retards fournisseurs, pipeline commercial, matrice de risque
- 🎯 **Funnel Chart** : analyse du pipeline CRM par stade de maturité
- 💰 **KPI Dashboard** : synthèse exécutive (pipeline, CA gagné, risques financiers)
- 📋 **Tables détaillées** : livraisons critiques, recommandations stratégiques
- 🔍 **Insights opérationnels** : anomalies CRM, valeurs bloquées, opportunités d'optimisation

**Durée d'exécution** : ~2-3 minutes pour l'intégralité du notebook.

---

# Dassault Aviation — S&OP Analytics 🛩️
> *Simulation d'une architecture Data complète (CRM × ERP × Python × Excel × Power BI) pour piloter la performance commerciale et logistique de l'industrie de la défense.*

---

## 📌 Contexte & Problématique

Ce projet simule une architecture Data orientée **Sales & Operations Planning (S&OP)** chez Dassault Aviation. Face à un carnet de commandes historique à l'export, l'objectif est d'identifier les goulots d'étranglement capacitaires de la Supply Chain, avec un focus sur le marché indien (politique du *"Make in India"*).

**Question clé :** Quels contrats commerciaux sont aujourd'hui financièrement à risque à cause des retards logistiques de notre supply chain indienne (Tata, HAL, Reliance) ?

---

## ⚙️ Stack Technique & Architecture

| Outil | Rôle |
|---|---|
| **Python (Pandas / NumPy)** | Nettoyage des données, EDA, détection d'anomalies |
| **Salesforce CRM** | Suivi du pipeline commercial (Leads, Comptes, Opportunités, Dashboards) |
| **SAP ERP (MM/SD)** | Opérations logistiques (PO, MIGO, VL01N, MIRO, Factures) |
| **Excel (Power Query / TCD)** | Modélisation relationnelle S&OP, reporting financier croisé |
| **Power BI** | Dashboards régionaux, KPI financiers, analyse O2C |

---

## PARTIE 1 — Audit des Retards Fournisseurs & Pipeline CRM
*(Python Pandas — `/notebooks`)*

### 1.1 Données utilisées

- **Retards fournisseurs (MIGO / ERP)** : 760 réceptions analysées, dont **428 en retard** (56 %)
- **Pipeline CRM (Salesforce)** : 1 200 deals en cours — montant total **307 Md€** (tous stades)

### 1.2 Retards par site de production

| Site de production | Retard moyen (j) |
|---|---|
| **Hyderabad** | 30,1 |
| **Bordeaux** | 24,9 |
| **Mérignac** | 21,8 |
| **Nagpur** | 21,8 |
| **Bangalore** | 18,4 |

### 1.3 Pipeline commercial — Répartition par stade

| Stade | Montant (Md€) |
|---|---|
| Proposal | 75,4 |
| Closed Won | 63,1 |
| Negotiation | 57,7 |
| Qualification | 44,7 |
| Prospecting | 36,7 |
| Closed Lost | 29,7 |
| **TOTAL** | **307,3** |

---

## PARTIE 2 — Livraisons ERP & Valeurs Bloquées

### 2.1 Clients avec valeurs bloquées

| Client | Valeur bloquée (Md€) |
|---|---|
| Reliance Industries | 7,02 |
| Indian Air Force | 4,56 |
| Indonesian Air Force | 4,05 |
| **TOTAL** | **15,63** |

### 2.2 Livraisons critiques retardées

| Livraison | Client | Produit | Retard | Montant bloqué |
|---|---|---|---|---|
| VL0080000029 | Indonesian Air Force | Rafale F3-R | **365 jours** | 783,5 M€ |
| VL0080000003 | Reliance Industries | Rafale F4 | 60 jours | 882 M€ |
| VL0080000005 | Air France | Falcon 10X | 90 jours | 301,6 M€ |

---

## Conclusion Exécutive

| Indicateur | Valeur |
|---|---|
| Pipeline commercial total | **307 Md€** |
| CA gagné | **48 Md€** |
| Risque financier (retards logistiques) | **41,29 Md€** |
| Valeurs bloquées (3 clients) | **15,63 Md€** |
| Anomalies P2P | **48,96 M€** |
| Cash at Risk O2C | **24 Md€** |
| Pipeline CRM dormant | **6,13 Mds€** |

---

*Stack : Python (Pandas, NumPy) · Salesforce CRM · SAP ERP (MM/SD) · Excel (Power Query, TCD) · Power BI*
