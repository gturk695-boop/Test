## Partie A. Python plus idiomatique

### A Q1. C'est quoi une compréhension de liste, quel avantage par rapport à une boucle for ?

Une compréhension de liste permet de construire une liste en une seule ligne à partir d'une autre, par exemple [t * 100 for t in taux]. On peut aussi y ajouter une condition, comme [v for v in variations if v > 0] pour ne garder que les hausses. Par rapport à une boucle "for" avec "append", c'est plus court et plus lisible, et un peu plus rapide. Dans notre notebook, le calcul des variations de la séance 2, qui prenait quatre lignes, tient en une seule et donne exactement la même liste. On peut faire la même chose avec un dictionnaire. Il ne faut quand même pas en abuser, car si la logique devient compliquée, une boucle classique reste plus claire.

### A Q2. À quoi servent enumerate et zip ?

"enumerate" donne à la fois la position et la valeur quand on parcourt une liste, ce qui évite d'écrire "range(len(taux))" puis "taux[i]". "zip" permet de parcourir plusieurs listes en même temps, élément par élément. On s'en est servi pour associer chaque date à son taux.

### A Q3. Comment trier une liste selon un critère ?

On utilise "sorted" avec le paramètre "key", qui indique sur quoi comparer les éléments. Pour trier nos couples (date, taux) selon le taux, on a écrit sorted(couples, key=lambda c: c[1]), et on ajoute "reverse=True" pour avoir l'ordre décroissant. "sorted" renvoie une nouvelle liste et ne modifie pas l'originale.

### A Q4. C'est quoi une f-string, comment afficher un nombre à deux décimales ?

Une f-string est une chaîne précédée d'un "f", dans laquelle on peut mettre des variables ou des calculs entre accolades, comme f"1 EUR = {taux} USD". C'est plus lisible que de coller des morceaux avec "+" et "str()". Pour afficher deux décimales, on écrit f"{taux:.2f}", ce qui transforme par exemple 1.159 en 1.16. On peut aussi formater un pourcentage ou une date de la même façon.

### A Q5. C'est quoi une fonction lambda ?

C'est une petite fonction sans nom, écrite en une seule ligne, par exemple "lambda x: x * 100". Elle ne contient qu'une seule expression, dont le résultat est renvoyé automatiquement. On l'utilise quand on a besoin d'une fonction très simple une seule fois, souvent comme paramètre d'une autre fonction, avec "key" dans "sorted", ou avec "map" pour appliquer un calcul à chaque élément et "filter" pour ne garder que certains éléments. Dès que la fonction est plus longue ou qu'on la réutilise, il vaut mieux l'écrire normalement avec "def".

## Partie B. Les classes

### B Q1. C'est quoi une classe, un objet, une instance, à quoi sert self ?

Une classe est un modèle qui regroupe des données, les attributs, et des fonctions qui agissent sur ces données, les méthodes. Notre classe "SerieTaux" regroupe par exemple une devise et ses taux, avec des méthodes comme "moyenne()" ou "variation()". Un objet est un exemplaire concret créé à partir de la classe, et une instance veut dire exactement la même chose. On peut en créer autant qu'on veut, et nous en avons créé une par devise, chacune avec ses propres taux. "self" représente l'objet sur lequel on appelle la méthode. Quand on écrit "usd.moyenne()", "self" désigne "usd", et c'est grâce à lui que la méthode accède aux taux de cet objet-là.

### B Q2. À quoi sert __init__ ?

"__init__" est la méthode appelée automatiquement quand on crée un objet. Elle sert à lui donner ses attributs de départ, à partir des valeurs qu'on lui passe. Quand on écrit SerieTaux("USD", taux), Python crée l'objet puis appelle "__init__", qui enregistre la devise et les taux dans l'objet.

### B Q3. Différence entre un attribut de classe et un attribut d'instance ?

Un attribut de classe est défini directement dans la classe, en dehors des méthodes, comme base = "EUR" dans "SerieTaux". Il est partagé par toutes les instances, donc "usd.base" et "gbp.base" valent tous les deux "EUR". Un attribut d'instance est défini dans "__init__" avec "self", comme "self.devise", et il est propre à chaque objet. Il faut faire attention avec une liste en attribut de classe. Comme elle est partagée, si un objet y ajoute un élément, tous les autres le voient aussi. C'est le même problème de partage que celui qu'on avait vu avec la copie des dictionnaires en séance 1. Pour avoir une liste par objet, il faut la créer dans "__init__".

### B Q4. Qu'apporte une dataclass ?

Avec "@dataclass", il suffit de lister les attributs avec leur type, et Python écrit tout seul la méthode "__init__". Il génère aussi un affichage lisible de l'objet quand on fait un "print", et la comparaison avec "==", qui considère comme égaux deux objets ayant les mêmes valeurs. Le code est plus court, avec moins de risques d'erreur, ce qui est pratique pour les classes qui servent surtout à stocker des données. Pour une liste par défaut, on utilise "field(default_factory=list)", qui crée une nouvelle liste pour chaque objet et évite le piège de la question précédente.

## Partie C. matplotlib

### C Q1. Différence entre la figure et les axes, pourquoi préférer fig, ax = plt.subplots() ?

La figure est l'image entière, le support sur lequel on dessine. Les axes correspondent à un graphique à l'intérieur de cette figure, avec ses axes x et y, sa courbe et son titre. Une même figure peut contenir plusieurs axes, comme dans notre graphique qui met côte à côte la comparaison des devises et l'histogramme. Avec "fig, ax = plt.subplots()", on garde une référence à chaque graphique et on sait toujours sur lequel on dessine. Si on utilise directement "plt.plot", pyplot dessine sur le graphique « en cours », et ça devient vite confus dès qu'il y en a plusieurs. C'est aussi ce qui nous a permis de mettre le code des graphiques dans des fonctions.

### C Q2. Quel type de graphique pour quel type de donnée ?

Pour une série temporelle, comme l'évolution d'un taux jour après jour, on utilise une courbe. Pour une distribution, comme la répartition des variations quotidiennes, on utilise un histogramme. Pour comparer des catégories, comme la moyenne de chaque devise, on utilise plutôt des barres. Et pour comparer des séries qui n'ont pas la même échelle, comme le dollar et la livre, on les ramène en base 100 sur une même courbe.

### C Q3. Comment sauvegarder une figure en PNG ?

On utilise fig.savefig("graphiques/eur_usd.png"). Nous avons ajouté "dpi=150" pour une meilleure qualité et bbox_inches="tight" pour que les titres ne soient pas coupés. Il faut appeler "savefig" avant "plt.show()", sinon l'image peut être vide.

## Partie D. Assembler et finaliser

### D Q1. À quoi sert argparse, pourquoi une ligne de commande plutôt que des input() ?

"argparse" lit les arguments qu'on donne au lancement du programme dans le terminal, par exemple "python main.py analyser --devise GBP". Il vérifie les arguments, prévoit des valeurs par défaut et crée automatiquement une aide avec "--help". Avec "input()", le programme s'arrête et attend que quelqu'un tape une réponse. Une ligne de commande peut au contraire être lancée automatiquement, par un autre script ou à heure fixe, sans personne devant l'écran. Elle est aussi reproductible, puisqu'on peut écrire la commande dans le README et que tout le monde lance exactement la même chose.

### D Q2. Que fait exactement if __name__ == "__main__" ?

Chaque fichier Python a une variable "__name__". Elle vaut "__main__" quand on lance le fichier directement, et le nom du module quand le fichier est importé par un autre. Dans notre notebook, "src.donnees.__name__" vaut par exemple "src.donnees". Le code placé sous cette condition ne s'exécute donc que si on lance le fichier, pas quand on l'importe. Ça permet de réutiliser les fonctions d'un fichier sans lancer tout le programme.

### D Q3. C'est quoi un module, un package ?

Un module est simplement un fichier ".py" dont on peut importer le contenu, comme "src/donnees.py", d'où l'on importe "charger_taux". Un package est un dossier qui regroupe plusieurs modules, avec un fichier "__init__.py" qui peut être vide. Notre dossier "src" est un package, ce qui nous permet de ranger le code par thème, avec les données, la classe et les graphiques, au lieu d'avoir un seul gros fichier.

### D Q4. Que doit contenir un bon README, à quoi servent requirements.txt et .gitignore ?

Un bon README explique rapidement ce que fait le projet et qui l'a réalisé, comment l'installer, comment l'utiliser avec des exemples de commandes, et comment le code est organisé. Le fichier "requirements.txt" liste les librairies dont le projet a besoin, avec leur version. Avec "pip install -r requirements.txt", n'importe qui installe le même environnement que nous, et le code fonctionne de la même façon chez tout le monde. Le fichier ".gitignore" indique à Git les fichiers à ne jamais enregistrer dans le dépôt, comme les fichiers générés automatiquement ("__pycache__", ".ipynb_checkpoints"), les fichiers propres à un ordinateur ou les fichiers de log. Le dépôt reste ainsi propre.
