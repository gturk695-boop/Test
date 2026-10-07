Rapport final — Projet d'analyse des taux de change



Objectif

Récupérer les taux de change de référence publiés par la BCE pour deux devises (dollar américain et livre sterling), 
du 1er janvier au 1er septembre 2026, puis les nettoyer, les analyser et les représenter graphiquement. 




Démarche

Ce projet a été développé au fil de 4 séances de Python, en partant de l'extraction de données de taux de change 
via l'API Frankfurter (EUR vers USD et GBP), jusqu'à leur analyse et leur visualisation.

Séance 1 : récupération des données
Les taux viennent de l'API Frankfurter (taux BCE, gratuite, sans clé), appelée 
avec urllib. La réponse brute est gardée dans cache/ pour ne pas rappeler l'API à chaque exécution, puis convertie 
en CSV dans donnees/. La série compte 171 jours de cotation. Elle commence le 31/12/2025, car le 1er janvier est 
férié et l'API renvoie le dernier taux disponible.

Séance 2 : fonctions et robustesse. 
Le traitement est découpé en fonctions (lecture du CSV, moyenne, min/max). L'appel à l'API est protégé par try/except 
(pas de connexion, erreur HTTP, réponse illisible) et suivi dans un fichier de log.

Séance 3 : pandas
Les données sont chargées dans un DataFrame. Les 4 jours fériés de la BCE (1er janvier, Vendredi saint, lundi de Pâques, 1er mai)
sont comblés par forward-fill, ce qui donne 175 jours ouvrés. Nous avons choisi le forward-fill parce qu'un jour férié, le dernier 
taux publié reste le taux de référence. Les deux devises sont ensuite réunies par une jointure sur la date.

Séance 4 : organisation finale 
Une classe SerieTaux regroupe les taux d'une devise et ses calculs. Le code est rangé dans src/ et piloté par main.py 
avec trois commandes, extraire, analyser et graphiques.




Graphiques produits

Tous les graphiques sont dans le dossier graphiques/ et couvrent toute la période, du 31/12/2025 au 01/09/2026.

- `eur_usd.png` et `eur_gbp.png` : évolution des taux EUR/USD et EUR/GBP, sous forme de courbe.
- `comparaison.png` : comparaison des deux taux en base 100 au 31/12/2025, pour pouvoir les comparer malgré leurs niveaux différents (1,17 dollar et 0,87 livre pour 1 euro).
- `histogramme_usd.png` et `histogramme_gbp.png` : distribution des variations quotidiennes en %.
- `comparaison_histogramme.png` : la comparaison en base 100 et l'histogramme EUR/USD affichés côte à côte (subplots).




Résultats

Devise	31/12/2025	01/09/2026	Variation
USD	    1,1750	     1,1590	      −1,36 %
GBP	    0,8726	     0,8566	      −1,84 %

Sur la période, l'euro a baissé face aux deux devises, un peu plus face à la livre que face au dollar. 

Le taux EUR/USD est le plus agité. Après une petite baisse début janvier, il monte nettement jusqu'à son plus haut de la période 
(1,1974 fin janvier), puis redescend par étapes jusqu'à la mi-mars. Il remonte autour de 100 en base 100 en avril et début mai, 
avant de chuter jusqu'à son plus bas (1,134 fin juin). Il reste bas en juillet, puis remonte surtout en août pour finir à 1,159, 
soit −1,36 % sur la période. Son taux moyen est de 1,1624.

Le taux EUR/GBP bouge beaucoup moins. En base 100, il reste entre 97 et 100,5 environ sur toute la période, contre un écart 
d'environ 96,5 à 102 pour le dollar. Il baisse surtout en juillet, atteint son point le plus bas vers la fin du mois, 
puis remonte légèrement en août pour finir à −1,84 %. Les deux courbes évoluent parfois dans le même sens, comme pendant 
l'été, où elles baissent toutes les deux avant de remonter en août, mais le dollar réagit beaucoup plus fortement.

L'histogramme des variations quotidiennes d'EUR/USD montre que la plupart des mouvements journaliers sont faibles, 
le plus souvent inférieurs à 0,5 % en valeur absolue et centrés autour de zéro. Quelques jours plus agités sortent du lot, 
avec des variations allant d'environ −1,1 % à +1,3 %.

Ce projet a permis de mettre en pratique l'ensemble de la chaîne de traitement de données : récupération via une API, nettoyage et analyse, 
puis visualisation, tout en structurant le code de façon plus professionnelle (classes, outil en ligne de commande).
