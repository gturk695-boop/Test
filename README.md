# Projet Python - BFA1

Récupération et analyse des taux de change de référence de la BCE (API Frankfurter) du 1er janvier au 1er septembre 2026, pour le dollar (USD) et la livre sterling (GBP).

**Membres du groupe** Maxime Roure, Sacha Piguet, Gabriel Turk

Projet de groupe, Magistère BFA1, 2026-2027.

## Installation

Python 3.11 ou plus récent, et Jupyter (ou VS Code) pour ouvrir les notebooks.

```bash
git clone https://github.com/gturk695-boop/Test.git
cd Test
pip install -r requirements.txt
```

## Utilisation

Le code est organisé en un notebook par séance. Ouvrir les notebooks dans l'ordre, en commençant par [Séance_1_Notebook.ipynb](S%C3%A9ance_1_Notebook.ipynb), et exécuter les cellules de haut en bas. Les données sont téléchargées depuis l'API Frankfurter, une connexion internet est donc nécessaire.

```bash
jupyter notebook Séance_1_Notebook.ipynb
```

## Contenu du dépôt

| Séance | Thème | Code | Réponses aux questions |
|---|---|---|---|
| Séance 1 | Bases de Python, Git, premier appel à l'API | [Séance_1_Notebook.ipynb](S%C3%A9ance_1_Notebook.ipynb) | [Séance_1 - questions](S%C3%A9ance_1%20-%20questions.md) |
| Séance 2 | Fonctions, try/except, logging, récursivité | [Séance_2_Notebook.ipynb](S%C3%A9ance_2_Notebook.ipynb) | [Séance_2 - questions](S%C3%A9ance_2%20-%20questions.md) |
| Séance 3 | pandas, jointures, numpy, polars | [Séance_3_Notebook.ipynb](S%C3%A9ance_3_Notebook.ipynb) | [Séance_3 - questions](S%C3%A9ance_3%20-%20questions.md) |
| Séance 4 | Python idiomatique, classes, matplotlib | [Séance_4_Notebook.ipynb](S%C3%A9ance_4_Notebook.ipynb) | [Séance_4 - questions](S%C3%A9ance_4%20-%20questions.md) |

**[Rapport final](S%C3%A9ance_4%20-%20Rapport%20Final.md)**

Graphiques produits en séance 4
- [graphique_usd.png](graphique_usd.png) évolution de l'EUR/USD
- [comparaison_usd_gbp.png](comparaison_usd_gbp.png) comparaison des deux devises
- [histogramme_variations.png](histogramme_variations.png) distribution des variations quotidiennes
- [subplots_usd_gbp.png](subplots_usd_gbp.png) graphiques côte à côte

## Principaux résultats (EUR/USD)

| | |
|---|---|
| Période | 2025-12-31 au 2026-09-01 |
| Moyenne | 1.1624 |
| Min / max | 1.1340 / 1.1974 |
| Variation | -1.36 % |

La série commence le 31 décembre 2025 car le 1er janvier est férié. La BCE ne publie pas ce jour-là et l'API renvoie la dernière valeur disponible.
