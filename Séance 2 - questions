# Notes — Séance 2

## Partie A — Les fonctions

**1. Pourquoi découper le code en fonctions ? Trois bénéfices concrets ?**
Trois bénéfices : (1) Réutilisabilité — on écrit un traitement une fois et on l'appelle partout où on en a besoin, sans dupliquer le code. (2) Lisibilité — un programme découpé en fonctions nommées explicitement est plus facile à comprendre qu'un long bloc de code. (3) Facilité de test et de correction — on peut tester et corriger une fonction isolément, sans devoir relire tout le programme.

**2. Différence entre paramètre et valeur de retour ? Que renvoie une fonction sans return ?**
Un paramètre est une donnée d'entrée que la fonction reçoit pour effectuer son traitement. La valeur de retour (via `return`) est la donnée de sortie que la fonction renvoie au code appelant. Une fonction sans `return` renvoie automatiquement la valeur spéciale `None` (qui signifie "rien"/"aucune valeur").

**3. C'est quoi une docstring, où la place-t-on ?**
Une docstring est une chaîne de caractères entre triples guillemets (`"""..."""`) placée juste après la ligne `def` d'une fonction, qui décrit brièvement ce que fait la fonction, ses paramètres et ce qu'elle renvoie. Elle sert de documentation directement accessible dans le code.

**4. Différence entre variable locale et variable globale ?**
Une variable locale est définie à l'intérieur d'une fonction et n'existe que pendant l'exécution de cette fonction — elle est inaccessible depuis l'extérieur. Une variable globale est définie en dehors de toute fonction, au niveau principal du script, et reste accessible (en lecture) depuis n'importe quelle fonction du fichier.

## Partie B — try/except et logging

**1. Pourquoi gérer les erreurs avec try/except ? Que se passe-t-il si une exception n'est pas gérée ? À quoi servent else et finally ?**
try/except permet d'anticiper les erreurs prévisibles (problèmes réseau, données invalides) et d'y réagir proprement plutôt que de laisser le programme s'arrêter brutalement. Si une exception n'est pas interceptée par un except correspondant, le programme s'arrête immédiatement et affiche un message d'erreur technique (traceback). Le bloc else s'exécute uniquement si aucune erreur ne s'est produite dans le try ; le bloc finally s'exécute systématiquement, qu'il y ait eu une erreur ou non, ce qui est utile pour du nettoyage (fermeture de fichier ou de connexion).

**2. Pourquoi un except: nu (sans préciser le type d'erreur) est-il déconseillé ?**
Un except: nu intercepte absolument toutes les erreurs possibles, y compris des erreurs de programmation totalement différentes de celles qu'on voulait gérer (par exemple une faute de frappe dans le nom d'une variable). Cela masque des bugs réels au lieu de les révéler, et rend le débogage beaucoup plus difficile puisqu'on ne sait plus quelle erreur a réellement été interceptée. Il vaut mieux préciser le(s) type(s) d'exception exact(s) qu'on veut gérer.

**3. C'est quoi logging ? Pourquoi le préférer à print dans un vrai programme ? Citez les niveaux de log et un usage de chacun.**
logging est un module de la bibliothèque standard qui permet d'enregistrer des messages avec un niveau de gravité, un horodatage automatique, et de les rediriger vers un fichier plutôt que seulement les afficher à l'écran. Contrairement à print, il permet de garder une trace persistante du déroulement d'un programme, filtrable par niveau de gravité, ce qui est indispensable pour surveiller un programme en conditions réelles. Niveaux : info pour le déroulement normal (ex: "requête envoyée avec succès"), warning pour un cas suspect mais non bloquant (ex: "valeur inhabituelle reçue"), error pour une véritable erreur ayant empêché une opération (ex: "échec de connexion au serveur").

## Partie C — Récursivité et complexité

**1. C'est quoi la récursivité ? Cas de base et cas récursif ? Que se passe-t-il si le cas de base est absent ?**
La récursivité est une technique où une fonction s'appelle elle-même pour résoudre un problème en le décomposant en une version plus petite du même problème. Le cas de base est la situation la plus simple, résolue directement sans nouvel appel — il arrête la récursion. Le cas récursif est l'appel de la fonction sur elle-même, avec une entrée qui se rapproche du cas de base. Sans cas de base, la fonction s'appellerait indéfiniment elle-même, jusqu'à provoquer une RecursionError (dépassement de la profondeur maximale d'appels autorisée).

**2. Pourquoi utiliser la récursivité ? Est-elle toujours le meilleur choix ? Contre-exemple précis ?**
La récursivité rend le code plus lisible pour des problèmes naturellement récursifs (factorielle, parcours d'arborescences). Ce n'est pas toujours le meilleur choix : fib_naive en est un contre-exemple précis — sa complexité exponentielle O(2ⁿ), due aux recalculs répétés, la rend beaucoup plus lente que fib_iteratif, qui résout le même problème en O(n) et sans mémoire supplémentaire.

**3. C'est quoi la complexité temporelle ? La complexité spatiale ? Que signifient O(n), O(n²), O(2ⁿ) ?**
La complexité temporelle mesure la croissance du nombre d'opérations en fonction de la taille n de l'entrée ; la complexité spatiale mesure la croissance de la mémoire utilisée. O(n) : le temps croît proportionnellement à n (une boucle simple). O(n²) : il croît au carré de n (deux boucles imbriquées). O(2ⁿ) : il double à chaque n supplémentaire — croissance exponentielle, cas de fib_naive.

**4. C'est quoi la mémoïsation ? Que fait functools.lru_cache ? Pourquoi Python limite-t-il la profondeur de récursion ?**
La mémoïsation stocke les résultats déjà calculés pour les réutiliser sans les recalculer. functools.lru_cache applique automatiquement cette technique à une fonction via un décorateur. Python limite la profondeur de récursion car chaque appel en attente occupe de la mémoire dans la pile d'appels ; sans limite, une récursion sans fin épuiserait la mémoire disponible — la limite provoque une RecursionError propre avant d'en arriver là.


