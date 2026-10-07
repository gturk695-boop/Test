# Projet Python
 
Récupération et analyse des taux de change de référence de la BCE (API Frankfurter) du 1er janvier au 1er septembre 2026, pour le dollar (USD), le yen (JPY) et la livre sterling (GBP).
 
Membres du groupe : Maxime, Sacha, Gabriel
 
Projet de groupe, Magistère BFA1, 2026-2027.
 
## Installation
 
Python 3.11 ou plus récent.
 
```bash
git clone https://github.com/gturk695-boop/Test.git
cd Test
pip install -r requirements.txt
```
 
## Utilisation
 
```bash
python main.py --help
python main.py extraire --devises USD JPY GBP      # télécharge les taux dans cache/
python main.py analyser --devise USD               # moyenne, min, max, variation
python main.py graphiques --devises USD JPY GBP    # PNG dans graphiques/
```
 
Exemple de sortie de `python main.py analyser --devise USD`
 
```
EUR/USD du 2025-12-31 au 2026-09-01
  moyenne   : 1.1624
  min / max : 1.1340 / 1.1974
  variation : -1.36 %
```
 
## Organisation
 
```
main.py              ligne de commande (argparse)
src/donnees.py       appel à l'API et cache
src/serie.py         classe SerieTaux
src/graphiques.py    graphiques matplotlib
cache/               réponses brutes de l'API (JSON)
donnees/             CSV des taux
graphiques/          figures PNG
docs/                notes des séances 1 à 4 et rapport final
seance1.ipynb ... seance4.ipynb    travail de chaque séance
```
 
## Documents
 
- [Rapport final](docs/rapport_final.md)
- Notes des séances : [1](docs/notes_seance1.md), [2](docs/notes_seance2.md), [3](docs/notes_seance3.md), [4](docs/notes_seance4.md)
