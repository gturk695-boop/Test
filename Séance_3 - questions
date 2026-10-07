## Comparaison avec la séance 2
 
Sur notre série EUR/USD de 171 jours, pandas donne exactement les mêmes résultats que nos fonctions de la séance 2, avec une moyenne de 1,16237, un minimum de 1,134 et un maximum de 1,1974. La différence se voit surtout dans le code. En séance 2, il fallait lire le CSV ligne par ligne, convertir chaque taux en nombre, puis écrire des boucles pour la moyenne, le minimum et le maximum. Avec pandas, "read_csv" charge le fichier directement avec les bons types, et chaque calcul tient en une ligne.
 
## Partie A. Découvrir pandas
 
### A Q1. DataFrame et Series
 
Un DataFrame est un tableau à deux dimensions, avec des lignes et des colonnes, un peu comme une feuille Excel. Chaque ligne a une étiquette, l'index, qui est la date dans notre cas, et chaque colonne a un nom, comme "USD". Une Series correspond à une seule colonne, par exemple df["USD"]. Un DataFrame est en fait un ensemble de Series qui partagent le même index.
 
### A Q2. Pourquoi pandas plutôt que des boucles et le module csv, vectorisation
 
pandas permet d'écrire beaucoup moins de code, il gère tout seul la lecture du fichier et les types, et il propose déjà les outils dont on a besoin en finance, comme les variations, les moyennes mobiles ou les jointures. Il est aussi plus rapide grâce à la vectorisation. Vectoriser, c'est appliquer une opération à toute une colonne d'un coup, par exemple df["USD"] * 100, au lieu d'écrire une boucle qui traite les valeurs une par une. Le calcul est alors fait en interne par numpy, dans un langage compilé, ce qui va beaucoup plus vite qu'une boucle Python.
 
### A Q3. Pourquoi déconseille-t-on iterrows() ?
 
"iterrows()" parcourt le DataFrame ligne par ligne avec une boucle Python, donc on perd tout l'intérêt de la vectorisation et ça devient très lent sur de grandes tables. En plus, chaque ligne est transformée en Series, ce qui peut changer le type des valeurs. Il vaut presque toujours mieux faire l'opération directement sur la colonne entière.
 
### A Q4. Valeurs manquantes (NaN), conséquences sur les moyennes
 
pandas note une valeur manquante "NaN", pour « Not a Number ». Chez nous, il y en avait 4 après avoir réindexé la série sur les jours ouvrés, une pour chaque jour férié de la BCE (le 1er janvier, le Vendredi saint, le lundi de Pâques et le 1er mai). Par défaut, "mean()", "sum()" ou "min()" ignorent les NaN, et la moyenne est donc calculée seulement sur les valeurs présentes. Ça évite une erreur, mais il faut garder en tête que la moyenne peut porter sur moins de jours qu'on ne le pense.
 
## Partie B. Nettoyer et analyser
 
### B.1 Pourquoi le forward-fill
 
Les jours fériés, la BCE ne publie pas de nouveau taux, donc le dernier taux publié reste le taux de référence jusqu'à la publication suivante. Il nous a donc paru logique de le reprendre, plutôt que de laisser un trou qui fausserait les calculs jour par jour ou d'inventer une valeur. Comme on ne comble que 4 jours sur 175, ça n'a presque aucun effet sur nos statistiques.
 
### B Q1. C'est quoi le forward-fill, quelle hypothèse ?
 
Le forward-fill, avec "ffill()", remplace chaque valeur manquante par la dernière valeur connue avant elle. Le taux du 1er janvier 2026 est par exemple remplacé par celui du 31 décembre 2025. L'hypothèse, c'est que le taux n'a pas changé pendant le jour manquant. Elle est raisonnable pour un jour férié, mais elle le serait beaucoup moins pour un long trou dans les données. Elle crée aussi des variations journalières égales à zéro, qu'on retrouve dans nos calculs avec numpy.
 
### B Q2. À quoi sert resample, c'est quoi une moyenne mobile ?
 
"resample" sert à changer la fréquence d'une série temporelle. Nous l'avons utilisé pour passer de données journalières à des données mensuelles, avec resample("ME").mean(), qui calcule la moyenne de chaque mois. Une moyenne mobile est une moyenne calculée sur une fenêtre qui avance dans le temps. Avec "rolling(window=5).mean()", chaque jour, on fait la moyenne des 5 derniers taux. Ça lisse la courbe et permet de mieux voir la tendance. Les 4 premières valeurs sont vides, puisqu'il n'y a pas encore 5 jours d'historique. Sur l'ensemble de la période, l'euro a perdu 1,36 % face au dollar, en passant de 1,175 à 1,159.
 
## Partie C. Les jointures
 
### C Q1. Les quatre types de jointure
 
Une jointure "inner" ne garde que les clés présentes dans les deux tables. Une jointure "left" garde toutes les lignes de la table de gauche et met des NaN à droite quand il n'y a pas de correspondance, et "right" fait l'inverse. Enfin, "outer" garde toutes les lignes des deux tables, avec des NaN des deux côtés si besoin. Dans notre exemple, avec les clés 1 et 2 à gauche et 2 et 3 à droite, "inner" ne garde que la clé 2, "left" garde 1 et 2, "right" garde 2 et 3, et "outer" garde les trois.
 
### C Q2. Sur quelle clé joint-on, que devient une ligne sans correspondance ?
 
On joint sur la colonne commune aux deux tables, la clé, qui est la date dans notre cas. Une ligne sans correspondance disparaît avec "inner". Avec "left", "right" ou "outer", elle est gardée si elle se trouve du côté conservé, et les colonnes de l'autre table sont remplies avec des NaN. Il faut aussi faire attention aux doublons, parce que si une clé apparaît plusieurs fois, la jointure fait toutes les combinaisons possibles. Deux lignes à gauche et trois à droite pour la même clé donnent six lignes, comme on l'a vérifié dans le notebook.
 
### C Q3. Quelle jointure pour deux séries de taux sur la même période ?
 
Comme nos séries ont été réindexées sur le même calendrier, les dates coïncident exactement, et toutes les jointures donnent le même résultat de 175 lignes. Nous avons gardé "inner", qui est le choix par défaut. Il garantit de n'avoir que des dates où l'on dispose de tous les taux, donc sans NaN, ce qui est ce qu'on veut pour comparer les devises jour par jour.
 
### C Q4. Différence entre merge et concat
 
"merge" associe les lignes de deux tables qui ont la même clé, un peu comme une RECHERCHEV dans Excel. On s'en sert pour mettre côte à côte des informations qui portent sur les mêmes dates. "concat" empile simplement des tables sans regarder de clé, soit les unes sous les autres, par exemple pour ajouter une nouvelle année de données à la suite, soit côte à côte. "join" est un raccourci de "merge" qui joint directement sur l'index.
 
## Partie D. numpy et polars
 
### D Q1. Liste Python et tableau numpy, dtype, broadcasting
 
Une liste Python peut mélanger des éléments de types différents, alors qu'un tableau numpy, appelé "ndarray", ne contient que des éléments du même type, rangés les uns à la suite des autres en mémoire. On peut aussi faire des calculs directement sur un tableau numpy, alors que "liste * 2" ne fait que répéter la liste. Le dtype est justement le type commun des éléments du tableau, "float64" pour nos taux. Le broadcasting, c'est le fait que numpy applique automatiquement une opération avec un nombre à tout le tableau. Par exemple, "usd_np * 100" multiplie chaque taux par 100 sans qu'on ait besoin d'écrire de boucle.
 
### D Q2. Pourquoi numpy est plus rapide que des boucles Python ?
 
numpy fait ses calculs en C, un langage compilé, au lieu de passer par l'interpréteur Python à chaque tour de boucle. Comme tous les éléments ont le même type, il n'a pas besoin de vérifier le type de chaque valeur. Et comme les données sont rangées à la suite en mémoire, le processeur peut les lire très rapidement.
 
### D Q3. pandas ou polars ?
 
polars est écrit en Rust et peut utiliser tous les cœurs du processeur en même temps, alors que pandas repose sur Python et numpy et travaille surtout sur un seul cœur. polars propose aussi une évaluation paresseuse, c'est-à-dire qu'il peut regarder toute la suite d'opérations avant de calculer quoi que ce soit, pour l'optimiser. Sa syntaxe est un peu plus longue, avec par exemple select(pl.col("USD").mean()) au lieu de df["USD"].mean(). Sur nos 175 lignes, les deux mettent quelques millisecondes et la différence ne veut pas dire grand-chose. pandas reste plus simple et compatible avec presque toutes les autres librairies, donc c'est le bon choix pour des données de notre taille. polars devient vraiment intéressant sur de très gros volumes, avec des millions de lignes.
