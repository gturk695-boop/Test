 ## Partie A. Premiers pas en Python
 
### A.2 Q1. C'est quoi Python, à quoi sert-il, compilé ou interprété ?
 
Python est un langage de programmation généraliste et open source. Il est assez facile à lire, et il existe des bibliothèques pour à peu près tout. C'est pour ça qu'il est autant utilisé en analyse de données et en finance (récupérer des prix, calculer des rendements, tester une stratégie), mais aussi en machine learning, pour automatiser des tâches ou pour faire du web.
 
C'est un langage interprété. Contrairement au C, on ne produit pas de fichier exécutable à l'avance, c'est l'interpréteur Python qui lit le code et l'exécute au moment où on le lance. En pratique, ça veut dire qu'une erreur n'apparaît que lorsque Python arrive sur la ligne en question.
 
### A.2 Q2. Comment installer Python et vérifier la version ?
 
On télécharge l'installateur sur python.org (version 3.11 ou plus récente), ou on installe Anaconda, qui contient déjà Python et les principales bibliothèques. Sous Windows, il ne faut pas oublier de cocher « Add python.exe to PATH » pendant l'installation.
 
Pour vérifier, on tape "python --version" dans un terminal ("python3 --version" sur Mac). Chez nous, la commande renvoie "Python 3.12.7", donc tout fonctionne. On peut aussi le vérifier depuis le code avec "import sys" puis "print(sys.version)".
 
### A.2 Q3. Les différentes façons de lancer du code Python
 
| Façon de lancer | Comment | Quand l'utiliser |
|---|---|---|
| Mode interactif | taper "python" dans le terminal | tester une ligne ou faire un calcul rapide |
| Script ".py" | "python hello_world.py" | lancer un programme complet, qu'on peut réutiliser |
| Notebook Jupyter | exécuter les cellules une par une | analyser des données étape par étape, en voyant les résultats au fur et à mesure |
| IDE (VS Code, PyCharm) | bouton « Run » | travailler sur un projet avec plusieurs fichiers |
 
Pour ce projet, on a surtout utilisé les notebooks, et le terminal pour lancer "hello_world.py".
 
### A.3 Q1. Types de base, typage dynamique et "3" + 4
 
Les types de base sont les entiers "int" (42), les décimaux "float" (1.0956), les chaînes de caractères "str" ("EUR"), les booléens "bool" (True ou False), les listes "list" ([1.08, 1.09]) et les dictionnaires "dict" ({"base": "EUR"}). Il existe aussi "tuple", "set" et "None".
 
Le typage dynamique veut dire qu'on n'a pas besoin de déclarer le type d'une variable. Python le déduit tout seul à partir de la valeur, au moment de l'exécution. Une même variable peut donc contenir un entier, puis une chaîne (x = 3 puis x = "trois").
 
"3" + 4 renvoie une erreur "TypeError". Le "+" sert à additionner des nombres mais aussi à coller des chaînes, et Python ne veut pas choisir à notre place. Il ne convertit jamais un type en un autre sans qu'on le lui demande (on dit qu'il est fortement typé). Pour que ça marche, il faut convertir soi-même. int("3") + 4 donne 7, et "3" + str(4) donne "34".
 
### A.4 Q1. Différence entre opérateur booléen et opérateur logique
 
En Python, ce sont en fait les mêmes, c'est-à-dire "and", "or" et "not". Ils servent à combiner des conditions et renvoient vrai ou faux.
 
La vraie différence est plutôt avec les opérateurs de comparaison ("==", "<", ">="...). Eux comparent deux valeurs et donnent un booléen, par exemple 1.08 > 1 donne True. Les opérateurs logiques viennent ensuite combiner plusieurs comparaisons, comme dans taux > 1 and taux < 1.1.
 
### A.6 Q1. Quand utiliser for et quand utiliser while ?
 
On utilise "for" quand on sait sur quoi on boucle, par exemple pour parcourir notre liste de taux ou les clés d'un dictionnaire, ou pour faire un nombre de tours connu ("for i in range(10)").
 
On utilise "while" quand on ne sait pas à l'avance combien de tours il faudra, et qu'on veut répéter tant qu'une condition est vraie. Dans notre notebook, on l'a utilisé pour savoir combien d'années il faut pour doubler un capital placé à 5 % (la réponse est 15 ans). Il faut juste faire attention à ce que la condition finisse par devenir fausse, sinon la boucle ne s'arrête jamais.
 
---
 
## Partie B. Git et GitHub
 
### B Q1. C'est quoi Git, c'est quoi GitHub, quelle différence ?
 
Git est un logiciel installé sur l'ordinateur qui garde l'historique d'un projet. À chaque commit, il enregistre une sorte de photo du projet à ce moment-là. Il fonctionne en local, sans internet.
 
GitHub est un site web qui héberge des projets Git en ligne. Il ajoute tout ce qui sert à travailler à plusieurs, comme les pull requests ou la gestion des collaborateurs.
 
Pour résumer, Git est l'outil et GitHub un service en ligne qui s'appuie dessus. On passe de l'un à l'autre avec "git push" (envoyer nos changements) et "git pull" (récupérer ceux des autres).
 
### B Q2. Pourquoi utiliser Git et GitHub ?
 
D'abord pour garder l'historique, puisque chaque commit indique ce qui a changé, quand et par qui. Ensuite pour pouvoir revenir en arrière si une modification casse le code. Ça évite aussi les fichiers du genre "analyse_v2_final_final.py".
 
C'est surtout utile pour travailler à plusieurs. Chacun peut avancer sur sa branche sans écraser le travail des autres, et on regroupe tout avec une pull request. Enfin, le dépôt en ligne sert de sauvegarde et permet à l'enseignante de suivre notre travail.
 
---
 
## Partie C. Les données et l'API
 
### C.1 Q1. Affecter une valeur à une clé qui existe déjà
 
L'ancienne valeur est simplement remplacée. Après reponse["date"] = "2099-01-01", il y a toujours une seule clé "date", et le dictionnaire a toujours 4 clés. Un dictionnaire ne peut pas contenir deux fois la même clé, chaque clé est unique.
 
### C.1 Q2. L'original est-il modifié après .copy() ?
 
Ça dépend de ce qu'on modifie. Si on change une valeur simple dans la copie, comme la date, l'original ne bouge pas. Par contre, si on change le taux à l'intérieur de "rates" dans la copie, l'original est modifié aussi.
 
C'est parce que ".copy()" crée bien un nouveau dictionnaire, mais ne recopie pas ce qu'il y a à l'intérieur. Le dictionnaire "rates" est donc le même objet dans l'original et dans la copie. Quand on le modifie d'un côté, on le voit forcément de l'autre.
 
### C.1 Q3. Mutabilité, copie superficielle et copie profonde
 
Un objet est mutable quand on peut le modifier directement, sans en créer un nouveau (par exemple, "append" ajoute un élément à une liste existante). Un objet immuable, lui, ne peut pas être modifié. Quand on a l'impression de le changer, Python crée en fait un nouvel objet (par exemple, ".upper()" renvoie une nouvelle chaîne).
 
Une copie superficielle, comme ".copy()", ne copie que le premier niveau, donc les objets imbriqués restent partagés. C'est exactement ce qui s'est passé avec "rates". Une copie profonde copie tout, y compris ce qui est imbriqué, et la copie devient complètement indépendante de l'original. On la fait avec copy.deepcopy(reponse), en important le module "copy".
 
### C.1 Q4. Types mutables et immuables
 
| Mutables | Immuables |
|---|---|
| "list", par exemple [1, 2] | "int", par exemple 42 |
| "dict", par exemple {"USD": 1.09} | "float", par exemple 1.0956 |
| "set", par exemple {1, 2} | "bool", par exemple True |
| | "str", par exemple "EUR" |
| | "tuple", par exemple (1, 2) |
 
### C.2 Q1. API, requête et format JSON
 
Une API est un moyen pour un programme de demander des données à un autre programme, en suivant des règles fixées à l'avance. Ici, l'API Frankfurter nous donne les taux de change de référence de la BCE.
 
Envoyer une requête, c'est envoyer un message au serveur par internet (avec le protocole HTTP). On utilise une requête "GET" sur une adresse qui précise ce qu'on veut, par exemple "?from=EUR&to=USD". Le serveur répond avec un code (200 si tout s'est bien passé, 404 ou 403 en cas de problème) et avec les données. En Python, on fait ça avec "urllib.request.urlopen".
 
Le JSON est un format texte très courant pour échanger des données. Le module "json" le transforme en objets Python avec "json.loads".
 
| JSON | Python |
|---|---|
| objet {...} | "dict" |
| tableau [...] | "list" |
| chaîne | "str" |
| nombre | "int" ou "float" |
| true / false | True / False |
| null | None |
 
En récupérant nos données du 1er janvier au 1er septembre 2026, on a remarqué que la série commence le 31 décembre 2025. Le 1er janvier est férié et la BCE ne publie rien, donc l'API renvoie le dernier taux disponible. Les week-ends et les jours fériés n'apparaissent pas du tout.
 
### C.2 Q2. Pourquoi enregistrer la réponse dans cache/ ?
 
Lire un fichier sur l'ordinateur est beaucoup plus rapide que de refaire un appel par internet. Le code continue aussi de fonctionner si la connexion ou l'API ne répondent pas.
 
C'est également plus respectueux de l'API, qu'on évite de solliciter avec les mêmes requêtes à chaque exécution. Tout le groupe travaille aussi sur exactement les mêmes données, ce qui rend les résultats reproductibles.
 
Enfin, on garde la réponse brute de côté. Si on fait une erreur en créant le CSV, on peut repartir de la source sans rappeler l'API.
