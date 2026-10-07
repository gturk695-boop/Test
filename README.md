# Projet Python - BFA1
 
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
 
## Documents
 
| Séance | Code | Réponses aux questions |
|---|---|---|
| Séance 1 | [Séance_1_Notebook.ipynb](S%C3%A9ance_1_Notebook.ipynb) | [Séance_1 - questions](S%C3%A9ance_1%20-%20questions) |
| Séance 2 | [Séance_2_Notebook.ipynb](S%C3%A9ance_2_Notebook.ipynb) | [Séance_2 - questions](S%C3%A9ance_2%20-%20questions) |
| Séance 3 | [Séance_3_Notebook.ipynb](S%C3%A9ance_3_Notebook.ipynb) | [Séance_3 - questions](S%C3%A9ance_3%20-%20questions) |
| Séance 4 | [Séance_4 - code](S%C3%A9ance_4%20-%20code) | [Séance_4 - questions](S%C3%A9ance_4%20-%20questions) |
 
**[Rapport final](S%C3%A9ance_4%20-%20Rapport%20Final)**
