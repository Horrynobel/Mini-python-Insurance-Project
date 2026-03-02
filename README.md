## insurance-portfolio-kpi-analysis

## Analyse de portefeuille d’assurance – KPIs et reporting

Ce projet montre une démarche complète d’analyse de portefeuille d’assurance avec Python et Jupyter Notebook, depuis le nettoyage des données jusqu’à la production de rapports prêts pour les métiers.

Objectif du projet
Une compagnie d’assurance souhaite mieux comprendre la performance de son portefeuille :

Quels produits génèrent le plus de sinistres ?

Quelles lignes sont rentables ou déficitaires ?

Quels segments de clients sont les plus risqués ?

Ce projet met en place une pipeline d’analyse permettant de suivre des KPIs clés (fréquence de sinistre, ratio de sinistres, primes moyennes…) et de produire des rapports lisibles pour les parties prenantes non techniques.

# Données
Le projet utilise un jeu de données synthétique représentant un portefeuille d’assurance, avec notamment :

° Informations contrat : policy_id, policy_type (Health, Auto, Home, Life), tenure_years.
° Démographie client : customer_age, gender, region.
° Exposition et tarification : premium_amount, sum_insured.
° Sinistres : claim_made, claim_amount.
° Canal de distribution : channel (Agent, Online, Branch).

Des variables dérivées sont ajoutées pour l’analyse :

° age_band (tranches d’âge).
° claim_severity (No Claim, Low, Medium, High, Very High).
° loss_ratio (sinistres / primes par contrat).
° premium_per_year (prime normalisée par la durée).

Ce que j’ai réalisé
1. Pipeline de nettoyage et préparation des données
Suppression des doublons et des valeurs incohérentes (âges hors bornes, valeurs négatives).

# Application de règles métier :

claim_amount = 0 quand claim_made = 0.

Imputation des montants de sinistres manquants (sinistre déclaré mais montant nul) par la médiane des sinistres positifs.

Création d’une fonction réutilisable clean_insurance_data() pour encapsuler tout le pipeline de nettoyage et de feature engineering.

# Définition et calcul des KPIs d’assurance
Fréquence de sinistre (claim rate) globale et par :

Type de police (policy_type).

Canal (channel).

Tranche d’âge (age_band).

Ratio de sinistres (loss ratio) = somme des sinistres / somme des primes, par produit.

Primes moyennes par canal, produit, segment d’âge.

Sévérité moyenne des sinistres (montant moyen conditionnel à un sinistre).

# Visualisation des KPIs

J’ai construit plusieurs visualisations avec Matplotlib / Seaborn :

Barres de fréquence de sinistre par type de police.

Barres de ratio de sinistres par type de police, avec ligne de break-even (loss ratio = 1).

Barres de prime moyenne par canal de distribution.

Histogramme + KDE de la distribution d’âge des clients.

Barres de fréquence de sinistre par tranche d’âge.

Ces graphiques sont utilisés à la fois dans un PDF multi‑pages et dans un fichier Excel structuré.

# Rapport PDF avec interprétations métier

J’ai généré un rapport PDF multi‑pages combinant :

Une page de synthèse exécutive (volume de polices, primes totales, sinistres totaux, ratio de sinistres global, etc.).

Des pages graphiques (KPIs par produit, canal, âge).

Des pages d’interprétation et de recommandations entre les graphiques, par exemple :

Produits avec forte fréquence de sinistre et/ou ratio de sinistres élevé.

Canaux qui apportent les primes les plus élevées.

Tranches d’âge plus risquées.

L’objectif est de délivrer un document directement exploitable par des profils non techniques (souscription, actuariat, direction).

5. Fichier Excel multi‑onglets pour les analystes
En parallèle du PDF, j’ai produit un fichier insurance_final_cleaned.xlsx structuré pour les analyses ad hoc :

Onglet Cleaned_Data : dataset final nettoyé avec toutes les colonnes dérivées.

KPI_Summary : tableau synthétique des indicateurs clés.

Summary_Statistics : statistiques descriptives (moyennes, médianes, min/max, etc.).

Policy_Breakdown : agrégats par type de police (nombre de contrats, primes, sinistres, loss ratio).

Channel_Breakdown : agrégats par canal.

Age_Breakdown : agrégats par tranche d’âge.

Les colonnes monétaires et de pourcentage sont formatées dans Excel (€, pourcentages), avec filtres et volets figés pour faciliter l’exploration.

Stack technique
Langage : Python (Jupyter Notebook).

Librairies principales :

pandas, numpy pour la préparation et l’agrégation des données.

matplotlib, seaborn pour les visualisations.

xlsxwriter via pandas.ExcelWriter pour la génération du fichier Excel.

(Optionnel) ydata-profiling pour générer un rapport EDA automatique au format HTML.

Organisation du projet :

notebooks/insurance_kpi_analysis.ipynb – notebook principal.

src/ – fonctions de nettoyage et de visualisation (si modularisé).

reports/ – PDF et Excel générés.

data/ – données brutes et/ou script de génération du dataset synthétique.

README.md, requirements.txt.

