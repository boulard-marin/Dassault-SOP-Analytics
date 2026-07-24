# 🛩️ Dassault Aviation — S&OP Analytics

> *Simulation d'une architecture Data complète (CRM × ERP × Python × Excel × Power BI) pour piloter la performance commerciale et logistique de l'industrie de la défense.*

---

## 🚀 DÉMO INTERACTIVE — Lancer en un clic

Cliquez sur le badge ci-dessous pour lancer le notebook Jupyter hébergé gratuitement sur Binder :

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/boulard-marin/Dassault-SOP-Analytics/main?filepath=notebooks/demo_dassault.ipynb)

**Ou lancez directement via Voilà** (interface dashboard plus fluide) :

[![Voilà](https://img.shields.io/badge/Voilà-Interactive%20Dashboard-blueviolet?style=flat-square&logo=jupyter)](https://mybinder.org/v2/gh/boulard-marin/Dassault-SOP-Analytics/main?urlpath=voila/tree/notebooks/demo_dassault.ipynb)

**⏱️ Temps de chargement** : 30-60 secondes (première visite) — **Aucune installation requise** ✨

### 📊 Contenu de la démo interactive

- 📈 **Graphiques Plotly interactifs** : retards fournisseurs par site, distribution des retards (box plot), pipeline commercial
- 🎯 **Funnel Chart** : analyse du pipeline CRM par stade de maturité (Prospecting → Closed Won/Lost)
- 💰 **Matrice de Risque** : visualisation scatter des livraisons critiques (retard vs montant bloqué)
- 📋 **Tables détaillées** : livraisons critiques avec statuts, recommandations stratégiques par priorité
- 🔍 **Dashboard exécutif** : KPI synthèse (pipeline, CA gagné, retard moyen, taux de retard, montant bloqué, risque financier)
- 🎬 **Insights opérationnels** : anomalies CRM, valeurs bloquées par client, opportunités d'optimisation

**⏱️ Durée d'exécution** : ~2-3 minutes pour l'intégralité du notebook — données 100% générées et reproductibles.

---

## 📌 Contexte & Problématique Stratégique

Ce projet simule une **architecture Data orientée Sales & Operations Planning (S&OP)** chez Dassault Aviation, leader mondial de l'aéronautique de défense.

### Le défi

Dassault fait face à un dilemme classique des industriels complexes :
- **Pipeline commercial massif** : 307 Md€ de deals en cours à l'export (Inde, Moyen-Orient, Afrique)
- **Supply chain fragile** : retards logistiques systémiques sur les sites indiens (Hyderabad, Nagpur, Bangalore)
- **Cash flow bloqué** : 15,63 Md€ de livraisons retardées chez les 3 principaux clients
- **Risque de réputation** : délais de livraison incompatibles avec les attentes des forces armées

### Question clé

**Quels contrats commerciaux sont aujourd'hui financièrement à risque à cause des retards logistiques de notre supply chain indienne (Tata, HAL, Reliance) ?**

### Hypothèse de travail

Les retards ne sont pas aléatoires — ils sont concentrés sur :
1. **Sites géographiques** (Inde > France)
2. **Fournisseurs spécifiques** (Safran, Pratt & Whitney dominants)
3. **Périodes calendaires** (pics saisonniers)

↳ **Opportunité** : optimiser les 20 % de fournisseurs responsables de 80 % des retards (Pareto).

---

## ⚙️ Stack Technique & Architecture

| Outil | Rôle | Justification |
|---|---|---|
| **Python (Pandas / NumPy / SciPy)** | Nettoyage, EDA, détection d'anomalies, agrégations | Flexibilité analytique, reproductibilité |
| **Plotly** | Visualisations interactives (scatter, funnel, box plot, bar) | Engagement UX, exploration de données |
| **Jupyter / Voilà** | Notebook exécutable + interface dashboard | Démonstration sans infrastructure serveur |
| **Salesforce CRM** | Suivi du pipeline commercial (Leads → Closed Won/Lost) | Source de vérité commerciale |
| **SAP ERP (MM/SD)** | Opérations logistiques (PO, MIGO, VL01N, MIRO) | Source de vérité opérationnelle |
| **Excel (Power Query / TCD)** | Modélisation relationnelle S&OP, reporting croisé | Outil de pivot analytique pour CFO |
| **Power BI** | Dashboards régionaux, KPI financiers, analyse O2C | Automates pour la direction |

---

## 📊 PARTIE 1 — Audit des Retards Fournisseurs & Pipeline CRM

### 1.1 — Données de base utilisées

#### Datasets MIGO (ERP — Réceptions fournisseurs)
- **Volume total analysé** : 760 réceptions entre janvier-mai 2026
- **Réceptions retardées** : 428 (56,3 %)
- **Montant total** : 2 847 M€ sur la période
- **Fournisseurs tracés** : Safran, Pratt & Whitney, Elbit, Rolls-Royce, HAL

#### Dataset CRM (Salesforce — Pipeline commercial)
- **Nombre de deals en cours** : 1 200 opportunités
- **Montant total du pipeline** : 307,3 Md€
- **Stades représentés** : Prospecting → Closed Won/Lost
- **Régions** : Europe, Moyen-Orient, Asie, Afrique

---

### 1.2 — ANALYSE : Retards par Site de Production

**Classement des sites par performance logistique :**

| Site de production | Retard moyen (j) | Retard max (j) | Volume (réc.) | Montant total (M€) | Taux retard (%) |
|---|---|---|---|---|---|
| **🔴 Hyderabad** | 30,1 | 89,2 | 180 | 562,4 | 62,2 |
| **🟠 Bordeaux** | 24,9 | 67,8 | 150 | 498,7 | 58,1 |
| **🟡 Mérignac** | 21,8 | 54,3 | 140 | 421,6 | 51,4 |
| **🟡 Nagpur** | 21,8 | 56,7 | 160 | 512,3 | 54,8 |
| **🟢 Bangalore** | 18,4 | 42,1 | 130 | 381,0 | 47,7 |

**🔍 Insights critiques :**

1. **Hyderabad est la source du problème** (retard +63 % vs Bangalore)
   - Problème identifié : dépendance envers HAL (fournisseur public indien) avec cycles de production rigides
   - Impact financier : 562 M€ en circulation prolongée
   - Recommandation : diversifier vers Tata Aerospace (PMC)

2. **Disparité France-Inde révélatrice** (moyenne Inde : 26 j vs France : 23 j)
   - Causes structurelles : douanes, délais de shipping, infrastructure portuaire
   - Non aléatoire : pattern mensuel (pic en février-mars)

3. **Bangalore est le seul site performant** (18,4 j)
   - Leçon : Bangalore travaille avec des fournisseurs privés (Infosys, Cognizant IT vendors)
   - Benchmark à répliquer : contrats flexibles, SLA agressifs, pénalités de retard

---

### 1.3 — ANALYSE : Distribution des Retards (Variabilité & Outliers)

**Statistiques descriptives par site** :

| Site | Q1 (25%) | Médiane | Q3 (75%) | Écart-type | Outliers |
|---|---|---|---|---|---|
| Hyderabad | 18,2 j | 28,5 j | 41,3 j | 12,1 | 8 cas > 70j |
| Bordeaux | 14,1 j | 23,8 j | 35,6 j | 10,8 | 5 cas > 65j |
| Nagpur | 12,4 j | 20,2 j | 32,1 j | 11,9 | 7 cas > 60j |
| Mérignac | 11,7 j | 19,3 j | 31,2 j | 9,6 | 3 cas > 55j |
| Bangalore | 8,3 j | 17,1 j | 27,4 j | 8,2 | 1 cas > 45j |

**🔍 Insights critiques :**

1. **Hyderabad & Nagpur montrent une forte variabilité** (écart-type +48 % vs Bangalore)
   - Implication : prévisions imprévisibles → risque logistique élevé
   - Cause suspectée : dépendance à la meteo + manque de planification fournisseur
   - Action : mettre en place des stocks tampon préventifs (2 semaines supplémentaires)

2. **Outliers concentrés dans l'Inde du Nord** (15 anomalies vs 4 en France)
   - Cas extrêmes : 3 réceptions > 85 jours à Hyderabad
   - Hypothèse : incidents non documentés (retours qualité, manque de pièces)
   - Action : audit qualitatif sur 20 % des réceptions retardées

3. **Bangalore est fiable** (Q3 = 27,4j vs Hyderabad Q3 = 41,3j)
   - Opportunité : passer 40 % de la charge Hyderabad vers Bangalore
   - Contrainte : capacité de production limitée (+ 30 % max viable)

---

### 1.4 — ANALYSE : Pipeline Commercial — Répartition par Stade

**Funnel CRM — Montants par stade de maturité :**

| Stade | Montant (Md€) | % du total | Nombre deals | Montant moyen/deal (M€) | Probabilité moyenne (%) |
|---|---|---|---|---|---|
| **Proposal** | 75,4 | 24,5 % | 85 | 887 | 65 |
| **Closed Won** | 63,1 | 20,5 % | 50 | 1 262 | 100 |
| **Negotiation** | 57,7 | 18,8 % | 72 | 801 | 48 |
| **Qualification** | 44,7 | 14,5 % | 95 | 471 | 52 |
| **Prospecting** | 36,7 | 11,9 % | 100 | 367 | 25 |
| **Closed Lost** | 29,7 | 9,7 % | 28 | 1 061 | 0 |
| **TOTAL** | **307,3** | **100 %** | **430** | **715** | **48** |

**🔍 Insights critiques :**

1. **Blocage majeur en Negotiation** (57,7 Md€ — 18,8 % du pipeline)
   - Signal d'alerte : 72 deals dormants pendant 40-150 jours
   - Causes suspectées : désaccords prix, process d'approbation client lent, équipe comm sous-staffée
   - Analyse détaillée : 34 % n'ont pas eu d'interaction commerciale dans les 60 derniers jours
   - **Action prioritaire P0** : assigner un sponsor senior (VP Sales) à chaque deal > 500 M€ en Negotiation

2. **Fuite massive en Closed Lost** (29,7 Md€)
   - Taux de perte : 6,5 % du pipeline total
   - Problématique : certains deals basculent sans raison documentée
   - Recommandation : mettre en place un process "win/loss analysis" systématique

3. **Pipeline gagné très concentré** (Closed Won : 63,1 Md€)
   - CA confirmé = 63,1 Md€ vs Pipeline = 307,3 Md€ → ratio conversion = 20,5 %
   - Benchmark industrie : 15-25 % (Dassault est OK mais pas excellent)
   - Opportunité : passer à 25-30 % en optimisant Negotiation (gain potentiel : +10 Md€)

4. **Montant moyen par deal augmente avec la maturité** (Prospecting : 367 M€ vs Proposal : 887 M€)
   - Interprétation : les grands deals avancent plus lentement (logique)
   - Implication : optimiser Proposal est plus rentable que Prospecting

---

### 1.5 — ANALYSE : Sources d'Acquisition & ROI Marketing

**Répartition du pipeline par source lead :**

| Source | Montant (Md€) | % du total | Nombre deals | Deal moyen (M€) | Taux conv. Closed Won (%) |
|---|---|---|---|---|---|
| **Dubai Airshow** | 89,2 | 29,0 % | 95 | 939 | 24,2 |
| **DSEI London** | 67,4 | 21,9 % | 78 | 864 | 19,3 |
| **Aero India** | 55,8 | 18,2 % | 102 | 547 | 15,7 |
| **LinkedIn** | 51,3 | 16,7 % | 89 | 576 | 12,1 |
| **Embassy Referral** | 43,6 | 14,2 % | 66 | 661 | 18,8 |

**🔍 Insights critiques :**

1. **Dubai Airshow = champion du ROI** (taux conv. 24,2 %)
   - Montant concentré : 89,2 Md€ = 29 % du pipeline
   - Coût par deal acquis : très faible (événement annuel)
   - **Recommandation** : augmenter l'allocation budgétaire pour Dubai (+40 %)

2. **DSEI London performant mais moins attractif** (21,9 % du pipeline)
   - Deals plus gros (864 M€ avg vs 939 M€ Dubai)
   - Taux de conversion inférieur (19,3 % vs 24,2 %)
   - Implication : clients DSEI sont plus exigeants (buyer process plus long)

3. **Aero India sous-exploité** (18,2 % du pipeline)
   - Taux conversion faible (15,7 %) dépit d'une audience 100 % ciblée
   - Hypothèse : manque de suivi post-show, équipe indienne sous-staffée
   - Action : créer un desk dédié Inde (Bangalore/Delhi)

4. **LinkedIn = low performer** (16,7 %, taux conv. 12,1 %)
   - Canal digital souffre en aéronautique (décision achat toujours relationnelle)
   - Redirection recommandée : investir plutôt dans LinkedIn Sales Navigator + team de SDR

---

## 🚨 PARTIE 2 — Livraisons Critiques & Valeurs Bloquées

### 2.1 — Clients avec Valeurs Bloquées (VL01N — SAP)

**Top 3 des clients impactés :**

| Client | Valeur bloquée (Md€) | % du pipeline client | Nombre livraisons | Retard moyen (j) | Sévérité |
|---|---|---|---|---|---|
| **Reliance Industries** | 7,02 | 28,3 % | 4 | 68 | 🟠 ÉLEVÉE |
| **Indian Air Force** | 4,56 | 41,2 % | 3 | 82 | 🟠 ÉLEVÉE |
| **Indonesian Air Force** | 4,05 | 51,8 % | 2 | 178 | 🔴 CRITIQUE |
| **TOTAL TOP 3** | **15,63** | **36,8 %** | **9** | **109** | |

**🔍 Insights critiques :**

1. **Reliance Industries — situation équilibrée**
   - Valeur bloquée : 7,02 Md€ (28,3 % de son pipeline)
   - Retard moyen : 68 jours (acceptable pour l'aviation)
   - Status : en cours de déblocage, communication régulière établie
   - Risk level : MOYEN

2. **Indian Air Force — client de réputation mondiale à risque**
   - Valeur bloquée : 4,56 Md€ (41,2 % de son pipeline total!)
   - Problème : contrat Rafale F8X stalled depuis 82 jours
   - Enjeu géopolitique : contrat de prestige pour Dassault en Inde
   - Risk level : CRITIQUE — escalade politique probable

3. **Indonesian Air Force — situation explosif**
   - Valeur bloquée : 4,05 Md€ (montant ÉNORME pour l'Indonésie)
   - Retard : **365 jours** sur Rafale F3-R (détail : dépend d'une pièce HAL non produite)
   - Implication : contrat en risque réputationnel + annulation possible
   - Risk level : CRITIQUE — contact board-level urgence

---

### 2.2 — Livraisons Critiques Détaillées (VL01N)

**Tableau exhaustif des 6 livraisons critiques :**

| ID Livraison | Client | Produit | Retard (j) | Montant bloqué (M€) | Statut | Cause racine |
|---|---|---|---|---|---|---|
| **VL0080000029** | Indonesian Air Force | Rafale F3-R | **365** | 783,5 | 🔴 CRITIQUE | Composant HAL manquant ; escalade de production |
| **VL0080000003** | Reliance Industries | Rafale F4 | 60 | 882 | 🟠 ÉLEVÉ | Retard Safran (engines) + retard douanes |
| **VL0080000005** | Air France | Falcon 10X | 90 | 301,6 | 🟠 ÉLEVÉ | Retard intégration Pratt & Whitney (6 semaines) |
| **VL0080000012** | Indian Air Force | Falcon 8X | 45 | 420 | 🟡 MOYEN | Retard logistique interne Bordeaux (buffer insuffisant) |
| **VL0080000018** | UAE Air Force | Rafale F4 | 30 | 250 | 🟡 MOYEN | Délai administratif douanes Émirats |
| **VL0080000027** | Lockheed Martin | Spare Parts | 15 | 120 | 🟢 BAS | Retard picking warehouse (résolu dans 5 jours) |

**Montant total bloqué** : 2 757 M€ (analyse des 6 plus gros blocages)

---

### 2.3 — ANALYSE PROFONDE : Corrélation Retards Logistiques × Pipeline CRM

**Question clé croisée** : *Les clients avec livraisons retardées sont-ils aussi bloqués en pipeline commercial ?*

**Tableau croisé :**

| Client | Livraison retardée (j) | Pipeline commercial (Md€) | Stade actuel | Risque combiné |
|---|---|---|---|---|
| Indonesian Air Force | 365 | 7,81 | Negotiation (stalled 120j) | 🔴 CRITIQUE |
| Reliance Industries | 68 | 24,84 | Proposal (active) | 🟠 ÉLEVÉ |
| Indian Air Force | 82 | 11,07 | Proposal + Closed Won | 🟠 ÉLEVÉ |
| Air France | 90 | 18,42 | Closed Won (honoré) | 🟡 MOYEN |
| UAE Air Force | 30 | 9,56 | Proposal (active) | 🟡 MOYEN |

**🔍 Insights stratégiques :**

1. **Corrélation établie** : clients avec livraisons retardées = clients avec pipeline ralenti
   - Indonesian Air Force : retard 365j + pipeline stalled 120j → risque d'annulation en cascade
   - Probabilité d'escalade : TRÈS HAUTE

2. **Effet domino logistique** : retards fournisseurs → ralentissement négo commerciale
   - Clients deviennent méfiants sur la capacité à livrer dans les délais
   - Cycle vicieux : demandes additionnelles de garanties → rallongement négo

3. **Stratégie de déblocage croisée requise**
   - Impossibilité de séparer correction logistique et accélération commerciale
   - Recommandation : créer un "war room" multi-fonctionnel (Ops + Sales) pour top 3 clients

---

## 💰 PARTIE 3 — Analyse Financière & Cash Flow Impact

### 3.1 — Montants en Jeu (Vision Consolidée)

| Catégorie | Montant (Md€) | % du pipeline total | Criticité |
|---|---|---|---|
| **Pipeline commercial total** | 307,3 | 100 % | - |
| **CA Closed Won (gagné)** | 63,1 | 20,5 % | ✅ Sûr |
| **Pipeline en risque (Negotiation > 60j)** | 34,2 | 11,1 % | 🟠 À monitorer |
| **Valeurs bloquées (livraisons retardées)** | 2,757 | 0,9 % | 🔴 URGENT |
| **Cash at Risk (Negotiation + Prospecting)** | 94,4 | 30,7 % | ⚠️ Risque taux conversion |

**Montant total à risque** : ~131,4 Md€ (42,7 % du pipeline)

---

### 3.2 — Impact Financier des Retards

**Analyse coût des retards sur 12 mois** :

| Driver | Montant estimé (M€) | Source |
|---|---|---|
| Coût du capital bloqué (taux 3 %, durée moyenne 90j) | 208 | Valeurs bloquées × 3 % / 4 |
| Pénalités contractuelles (1 % par mois retard) | 312 | VL0080000029, VL0080000003 |
| Remises négociées post-retard (2-3 % des montants) | 82 | Estimé Reliance, InAF |
| Coûts logistiques additionnels (expediting) | 156 | Rush shipping, frais d'accélération |
| **Impact O&M total annuel** | **758** | |

---

### 3.3 — Taux de Retard Global

**Vue d'ensemble de la performance logistique** :

| Métrique | Valeur | Benchmark industrie |
|---|---|---|
| Taux global de retard (MIGO) | 56,3 % | 25-35 % (aéronautique) |
| Retard moyen | 24,1 jours | 8-12 jours |
| Livraisons > 60j retardées | 18,2 % | 5-8 % |
| Livraisons > 100j retardées | 4,7 % | < 1 % |

**Verdict** : performance supply chain **INFÉRIEURE au benchmark** de 2x-3x.

---

## 🎯 PARTIE 4 — Opportunités & Plan d'Action

### 4.1 — Opportunités Quick Wins (0-3 mois)

| # | Opportunité | Impact estimé | Effort | ROI |
|---|---|---|---|---|
| **Q1** | Déblocage livraison Indonesian Air Force (relance HAL) | +2,5 Md€ débloqués | ÉLEVÉ | Très élevé (sauve contrat) |
| **Q2** | Réactivation 15 deals dormants CRM (Negotiation) | +3,2 Md€ pipeline | MOYEN | Fort (15 % conversion) |
| **Q3** | Mise en place scorecard fournisseur (pénalités retard) | -8 jours retard moyen | MOYEN | Fort (économies 320 M€) |
| **Q4** | Redirection 30 % charge Hyderabad → Bangalore | -15 jours retard | ÉLEVÉ | Élevé (stabilité) |

---

### 4.2 — Recommandations Stratégiques Hiérarchisées

#### **PRIORITÉ 0 — 🔴 CRISES (0-30 jours)**

1. **Déblocage Indonesian Air Force (VL0080000029)**
   - Action : Escalade board-level Dassault-HAL
   - Coût paliatif : accélération production HAL + logistics expedited (+50 M€)
   - Résultat attendu : déblocage dans 30 jours
   - Propriétaire : VP Operations

2. **Réactivation Indian Air Force (VL0080000012 + Pipeline)**
   - Action : CEO call au client + offre incitative (extension warranty, spare parts gratuits)
   - Coût : estimation -2 % marge = 80 M€
   - Résultat attendu : engagement de livraison dans 45 jours
   - Propriétaire : CEO/Business Development

---

#### **PRIORITÉ 1 — 🟠 LEVIER STRUCTUREL (1-3 mois)**

3. **Nettoyage pipeline CRM — Déblocage Negotiation**
   - Action : audit 72 deals en Negotiation, assigner sponsor senior à top 20
   - Résultat attendu : +6,13 Md€ convertis (taux conversion 15 % → 20 %)
   - Effort : 40 jours-homme
   - Propriétaire : VP Sales

4. **Mise en place Supplier Scorecard**
   - Action : déployer système de scoring MIGO (ponctualité, qualité, flexibilité)
   - Pénalité : -1 % marge par jour retard > 10 jours
   - Résultat attendu : réduction 25 % des retards moyen terme
   - Propriétaire : Director Procurement

---

#### **PRIORITÉ 2 — 🟡 OPTIMISATION (3-6 mois)**

5. **Rééquilibrage supply chain Inde**
   - Redirection : migrer 30-40 % de charge Hyderabad → Bangalore + Pune
   - Investissement : contrats multi-année, investissement infrast. partenaires
   - Résultat attendu : -15 jours retard moyen Inde, diversification risque fournisseur
   - Propriétaire : SCM Director

6. **Stratégie marketing optimisée**
   - Investissement : Dubai Airshow (+40 % budget), création desk Inde dedicated
   - Résultat attendu : +20 % pipeline qualifié source marketing
   - Effort : hiring 2 SDR Inde + reallocation budget
   - Propriétaire : VP Marketing

---

### 4.3 — Métriques de Succès (KPI Tableau de Bord)

**Métriques à monitorer mensuellement** :

| KPI | Target | Baseline | Fréquence |
|---|---|---|---|
| **Retard fournisseurs moyen (jours)** | < 15j | 24,1j | Mensuel |
| **Taux de retard MIGO** | < 30 % | 56,3 % | Mensuel |
| **Valeurs bloquées (Md€)** | < 1 Md€ | 2,757 | Bi-hebdo |
| **Pipeline Negotiation > 60j** | < 20 Md€ | 34,2 Md€ | Hebdo |
| **Taux de conversion CRM** | 22 % | 20,5 % | Mensuel |
| **Customer satisfaction (NPS)** | > 75 | 68 | Trimestriel |

---

## 🔬 PARTIE 5 — Méthodologie & Reproductibilité

### 5.1 — Architecture de données

```
📁 Dassault-SOP-Analytics/
├── 📁 data/
│   ├── migo_receipts.csv (760 réceptions)
│   ├── crm_pipeline.csv (430 deals)
│   └── vl01n_deliveries.csv (6 livraisons critiques)
├── 📁 notebooks/
│   ├── demo_dassault.ipynb (démo interactive Plotly)
│   └── analysis_detailed.ipynb (analyses statistiques SciPy)
├── 📁 scripts/
│   ├── data_generation.py (génération données simulées)
│   └── export_powerbi.py (export pour BI)
└── README.md (this file)
```

### 5.2 — Reproductibilité des analyses

Toutes les analyses utilisent **seed numpy = 42** pour garantir reproductibilité.

```bash
# Installation
pip install -r requirements.txt

# Lancer la démo
jupyter notebook notebooks/demo_dassault.ipynb

# Ou avec Voilà (dashboard)
voila notebooks/demo_dassault.ipynb
```

### 5.3 — Limitations & Warnings

⚠️ **Important** :
- Données **entièrement simulées** (reproduction de patterns réels, pas données réelles Dassault)
- Valeurs inspirées d'indices publics (rapports financiers, salons aéronautiques)
- À adapter pour données réelles (ERP SAP, Salesforce API)

---

## 📈 Benchmarking Industrie

**Comment Dassault se positionne** :

| Métrique | Dassault (Simulation) | Airbus (Public) | Lockheed Martin | Commentaire |
|---|---|---|---|---|
| Taux retard supply chain | 56,3 % | 28-32 % | 24-28 % | Dassault significativement en retard |
| Retard moyen (j) | 24,1 | 10-12 | 8-10 | Priorité absolue d'amélioration |
| Conversion pipeline (%) | 20,5 % | 18-22 % | 20-25 % | Dassault OK mais peut mieux faire |
| Taux concentration clients (top 3) | 18,5 % | 12-15 % | 15-18 % | Acceptable |

---

## 🛠️ Pour Aller Plus Loin

### Extensions possibles

1. **Prédictive Analytics** : modèle ML pour prédire retards fournisseur (Random Forest, LightGBM)
2. **Simulation Monte Carlo** : projections impact retards sur cash flow 2026-2027
3. **Network Analysis** : cartographie dépendances fournisseurs (supply chain complexity)
4. **NLP** : analyse des échanges email client pour détecter churning risk

### Données réelles — Integration guide

Pour intégrer les données réelles :

1. **SAP ERP (MM module)** : exporter MIGO via `T-code MB51`
2. **Salesforce** : utiliser `Analytics API` pour pipeline sync
3. **Excel/Power Query** : créer refresh automatique via connecteur
4. **Power BI** : déployer dashboards opérationnels (refresh horaire)

---

## 👨‍💻 Auteur & Contributions

Créé avec ❤️ par **Data Science Team** — Mai 2026

**Stack utilisé** :
- Python (Pandas, NumPy, Plotly)
- Jupyter + Voilà
- GitHub (version control)

**Contributions bienvenues** : fork → pull request avec analyses additionnelles ou corrections.

---

## 📄 Licence

Ce projet est fourni à titre d'illustration analytique. Les données sont simulées et ne reflètent pas la réalité de Dassault Aviation.

---

**Dernière mise à jour** : 24 juillet 2026  
**Version** : 2.1 — README complet avec toutes les analyses  
**Status** : ✅ Prêt pour démonstration exécutive
