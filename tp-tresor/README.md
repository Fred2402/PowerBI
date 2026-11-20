# Dashboard Trésor : trajectoire des finances publiques françaises

Projet du module Conception de Dashboard (M2 Data & IA, Nexa Digital School).

## Contexte
Commanditaire : Direction générale du Trésor. Le ministre prépare un discours sur la trajectoire des finances publiques.

Questions traitées :
1. Où se situe la France par rapport à ses voisins et à la zone euro, et cette position s'est-elle dégradée ?
2. D'où vient le déficit français : des dépenses, des recettes ou de la charge de la dette ?
3. Les marchés font-ils payer à la France son financement plus cher qu'avant ?

## Message principal
La France est plus endettée que ses voisins (119,1 % du PIB, 3e dette de l'UE), son déficit (5,0 % du PIB) vient des dépenses plutôt que des recettes, et l'écart de taux avec l'Allemagne remonte à 1,47 point, proche du niveau de 2012.

## Données
Eurostat, 27 pays de l'UE, UE 27 et zone euro (EA21), depuis 2000 :
- dette publique trimestrielle (`gov_10q_ggdebt`)
- comptes publics trimestriels : solde, recettes, dépenses, charge d'intérêts (`gov_10q_ggnfa`)
- taux d'emprunt à 10 ans mensuels (`irt_lt_mcby_m`)

## Contenu
| Fichier | Rôle |
| --- | --- |
| `tp-tresor_powerbi.pbix` | Rapport Power BI (3 pages : L'essentiel, Les preuves, Annexes) |
| `notebooks/nettoyage_eurostat.ipynb` | Nettoyage Python des CSV Eurostat et export Excel |
| `theme/theme_tresor_bleu_jaune.json` | Thème Power BI (France en bleu, comparaisons en gris, seuils en jaune) |
| `maquette/maquette_dashboard_tresor.pdf` | Maquette de conception (valeurs indicatives) |
| `oral/presentation.md` | Texte de l'oral de 5 minutes |

## Pipeline
1. **Nettoyage (Python)** : colonnes utiles, conversion numérique, filtre UE 27 + agrégats, pivot (un indicateur par colonne), dates, libellés pays, solde primaire, moyenne trimestrielle des taux, contrôles qualité, export Excel.
2. **Modèle (Power BI)** : schéma en étoile, tables de faits Dette, Comptes, Taux, Taux_trimestriel ; dimensions Pays et Calendrier ; relations 1 vers plusieurs, filtrage à sens unique.
3. **Mesures (DAX)** : dette au dernier trimestre (stock), solde, recettes, dépenses et intérêts sur 4 trimestres glissants (flux), écart de taux avec l'Allemagne au dernier mois commun, décomposition de l'écart de solde France − zone euro.

## Lancer le nettoyage
1. Placer `dette.csv`, `comptes.csv` et `taux.csv` (téléchargés depuis l'API Eurostat) dans `notebooks/donnees/`.
2. Installer les dépendances : `pip install pandas openpyxl`.
3. Exécuter le notebook : les fichiers propres sont écrits dans `notebooks/donnees_propres/`.

## Limites
- Déficit total, pas structurel.
- Pas de charge d'intérêts pour la zone euro dans les données : intérêts présentés pour la France seule.
- L'Allemagne sert de référence pour le critère de taux (pas de données d'inflation).
- Données Eurostat révisables.

## Technologies
Python (pandas, openpyxl) · Power BI · Power Query · DAX
