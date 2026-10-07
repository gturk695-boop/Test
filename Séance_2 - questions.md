## Partie A. Les fonctions
 
### A Q1. Pourquoi découper le code en fonctions ?
 
D'abord pour ne pas répéter le même code. On écrit "moyenne()" une seule fois et on peut ensuite l'utiliser sur n'importe quelle liste de taux. Ensuite, le code devient plus lisible, puisque chaque fonction a un nom qui dit ce qu'elle fait. Enfin, c'est plus facile de vérifier et de corriger. On a par exemple pu tester notre fonction "moyenne()" toute seule en la comparant à "statistics.mean", et si on trouve une erreur, on la corrige à un seul endroit.
 
### A Q2. Paramètre et valeur de retour, fonction sans return
 
Le paramètre, c'est ce qu'on donne à la fonction en entrée, comme la liste de taux dans "moyenne(liste_taux)". La valeur de retour, c'est le résultat que la fonction renvoie avec "return", qu'on peut ensuite garder dans une variable. Une fonction sans "return" renvoie "None". C'est le cas d'une fonction qui fait seulement un "print", elle affiche quelque chose mais ne renvoie rien qu'on puisse réutiliser.
 
### A Q3. Qu'est-ce qu'une docstring ?
 
C'est une courte description de la fonction, écrite entre triples guillemets juste en dessous de la ligne "def". Elle explique ce que fait la fonction, et on peut l'afficher avec "help(moyenne)".
 
### A Q4. Variable locale et variable globale
 
Une variable locale est créée à l'intérieur d'une fonction et n'existe que pendant que la fonction s'exécute. Une variable globale est créée en dehors de toute fonction et peut être lue partout. Si on donne dans une fonction une valeur à une variable qui porte le même nom qu'une globale, Python crée en fait une nouvelle variable locale, et la globale ne change pas. On l'a vérifié dans le notebook, où "devise" reste "USD" après l'appel de la fonction. Pour modifier une globale depuis une fonction, il faudrait écrire "global", mais il vaut mieux passer la valeur en paramètre et la récupérer avec "return".
 
Pour la partie A.2, notre moyenne et celle de "statistics.mean" sont identiques, à une toute petite différence près vers la quinzième décimale. Elle vient des arrondis des nombres décimaux en machine et ne change rien pour nos taux.
 
## Partie B. Erreurs et logging
 
### B Q1. Pourquoi try/except, exception non gérée, else et finally
 
Certaines erreurs ne viennent pas de notre code, comme une coupure de connexion ou un serveur qui ne répond pas. "try/except" permet de les prévoir et de réagir proprement, en affichant un message clair au lieu de laisser le programme planter. Si une exception n'est pas gérée, Python arrête tout de suite le programme et affiche le message d'erreur, et la suite n'est jamais exécutée. Le bloc "else" s'exécute seulement si tout s'est bien passé dans le "try", alors que "finally" s'exécute dans tous les cas, qu'il y ait eu une erreur ou non. Dans notre fonction d'appel à l'API, on s'en sert pour noter dans le log que l'appel est terminé.
 
### B Q2. Pourquoi un except nu est déconseillé ?
 
Un "except:" sans type attrape absolument toutes les erreurs, même celles qu'on n'avait pas prévues, comme une faute de frappe dans un nom de variable. Le bug est alors caché et le programme continue comme si de rien n'était. Il vaut mieux préciser le type d'erreur, comme "HTTPError" ou "URLError", pour traiter chaque cas avec le bon message et laisser les vraies erreurs apparaître.
 
### B Q3. C'est quoi logging, pourquoi le préférer à print, les niveaux
 
"logging" est un module de Python qui enregistre ce qui se passe pendant l'exécution du programme, avec la date et un niveau d'importance, ici dans le fichier "seance2.log". On le préfère à "print" parce que les messages sont gardés dans un fichier qu'on peut relire après coup, et parce qu'on peut trier les messages selon leur importance. Il y a cinq niveaux. "DEBUG" sert aux détails pour chercher un bug, "INFO" au déroulement normal (par exemple « appel de l'API »), "WARNING" à un cas suspect qui n'empêche pas de continuer (chez nous, un taux qui n'est pas daté du jour), "ERROR" à une opération qui a échoué (une erreur 404 ou une absence de connexion), et "CRITICAL" à une erreur si grave que le programme ne peut plus continuer.
 
## Partie C. Récursivité et complexité
 
### C Q1. Récursivité, cas de base, cas récursif
 
Une fonction récursive est une fonction qui s'appelle elle-même pour résoudre une version plus petite du même problème, comme la factorielle, puisque n! = n × (n-1)!. Le cas de base est le cas simple où on connaît directement la réponse, et c'est lui qui arrête les appels (pour la factorielle, 0! = 1). Le cas récursif est celui où la fonction se rappelle sur un problème plus petit, qui se rapproche du cas de base. Sans cas de base, la fonction s'appellerait à l'infini, et Python finit par s'arrêter avec une "RecursionError" quand on dépasse 1000 appels imbriqués.
 
### C Q2. Pourquoi la récursivité, est-ce toujours le meilleur choix ?
 
La récursivité est pratique quand un problème se découpe naturellement en sous-problèmes du même type, parce que le code reste court et proche de la formule mathématique. Mais ce n'est pas toujours le bon choix. Notre contre-exemple, c'est Fibonacci en version récursive naïve. Pour calculer fib(30), elle fait 2 692 537 appels et met environ 200 ms, parce qu'elle recalcule sans arrêt les mêmes valeurs. Une simple boucle fait le même calcul en 30 tours, en quelques millièmes de milliseconde. En plus, la récursivité est limitée en profondeur, et la version mémoïsée plante sur fib(5000) alors que la version avec une boucle le calcule sans problème.
 
### C Q3. Complexité temporelle et spatiale, O(n), O(n²), O(2ⁿ)
 
La complexité temporelle mesure comment le nombre d'opérations, et donc le temps, augmente quand la taille n des données augmente. La complexité spatiale mesure de la même façon la mémoire supplémentaire utilisée. O(n) veut dire que si n double, le travail double aussi, comme pour une boucle simple qui calcule une moyenne. O(n²) veut dire que si n double, le travail est multiplié par quatre, comme avec deux boucles imbriquées. On l'a vu dans le notebook, avec 100 opérations pour n = 10 et 400 pour n = 20. O(2ⁿ) veut dire qu'ajouter 1 à n multiplie le travail par 2 au maximum, et ça devient vite impossible. Pour notre Fibonacci naïf, le temps était multiplié par environ 1,6 à chaque fois qu'on ajoutait 1 à n, ce qui reste bien une croissance exponentielle.
 
### C Q4. Mémoïsation, lru_cache, limite de récursion
 
La mémoïsation consiste à garder en mémoire les résultats déjà calculés pour ne pas les recalculer. "functools.lru_cache" le fait automatiquement, il suffit d'écrire "@lru_cache" au-dessus de la fonction. Avec ça, Fibonacci passe d'un temps exponentiel à un temps linéaire, en échange d'un peu de mémoire pour stocker les résultats. Python limite la profondeur de récursion à 1000 par défaut, parce que chaque appel en attente occupe de la mémoire. Sans limite, une récursion infinie finirait par saturer la mémoire et faire planter Python, alors qu'avec la limite on obtient une erreur claire.
 
## Mesures
 
Nos mesures montrent bien l'explosion de la version naïve de Fibonacci. Le temps passe d'environ 0,02 ms pour n = 10 à 2 ms pour n = 20, puis à environ 200 ms pour n = 30 et 600 ms pour n = 32, avec plus de 7 millions d'appels pour ce dernier cas. Pour n = 30, la version mémoïsée met environ 0,02 ms et la version itérative environ 0,004 ms. Pour n = 5000, seule la version itérative fonctionne (environ 0,5 ms), la version mémoïsée provoquant une "RecursionError". Côté mémoire, la version naïve et la version mémoïsée empilent jusqu'à n appels en attente, la seconde gardant en plus n + 1 valeurs dans son cache, alors que la version itérative n'utilise que deux variables. La version itérative est donc à la fois la plus rapide et la plus économe.

