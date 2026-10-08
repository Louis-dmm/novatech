#Reponse TP git :
Mission 5 :
- 
- Création de la page : `18ae4c5` Creation de la page contact.html
- Ajout du formulaire : `9734e08` Ajout du formulaire dans contact.html
- 6 commit au total
- git log --oneline --graph --all
- git show 9734e08 : permet d'afficher les métadonnées détaillées (auteur, date, message de commit) ainsi que le `diff` précis (lignes ajoutées / supprimées) de ce commit.


Mission 8 & 9 :
-  commande : git reset --MIXED HEAD~1
-  Le mode `--mixed` par défaut replace le pointeur HEAD sur le commit précédent et vide la zone de staging, mais préserve les modifications dans la zone de travail
-   git reset --hard HEAD~1` (mode destructif qui écrase le répertoire de travail) est une autre méthode
-   Pour un commit local, `git reset` est adapté car il réécrit l'historique sans impacter d'autres développeurs. Pour un commit    partagé sur GitHub, réécrire l'historique créerait   
 des conflits majeurs chez les collaborateurs. On utilise donc `git revert`, qui est non destructif : il crée un nouveau commit qui applique la modification inverse tout en conservant la traçabilité complète.

Mision 11 :
- git cherry-pick 1e261b1
- Id du commit : 1e261b1
- git merge test-experiments aurait intégré l'intégralité des 3 commits de la branche (y compris les tests de couleurs et de footer qu'on ne voualit pas sur main)
.git cherry-pick tu récupères juste le commit du fix sans toucher au reste.

Mission 12 :
- Les 3 nombres représentent : MAJEURE.MINEURE.CORRECTIF : Changement majeur de structure (EX:passage a IOS27). Ajout de fonctionnalité. Correction de bugs
- Versions suivantes : - Correction de bug mineures : v1.0.1
                        - nouvellee fonctionnalité compatible : v1.1.0
                    - Refonte majeure incompatible : v2.0.0

#Questions :
1) La zone de travail correspond aux fichiers réels présents sur le disque, ou l'on modifie son code.
La zone de staging (l'index) sert d'étape intermédiaire : on y place avec `git add` uniquement les fichiers qu'on a choisis pour le prochain commit.
L'historique (le dépôt Git), c'est la base de données locale dans `.git` qui stocke définitivement tous les commits validés.
2) Cela permet d'isoler son code en cours pour ne pas casser la branche `main`, qui doit toujours rester propre et fonctionnelle. C'est aussi indispensable pour faire tester ou relire son code dans une Pull Request sur GitHub avant de l'intégrer au projet principal.
3) `git reset` réécrit l'histoire : il fait reculer le pointeur de la branche et retire le commit de la vue courante. C'est adapté quand le commit est resté en local.
`git revert`, au contraire, ne supprime rien : il avance dans l'historique en créant un nouveau commit qui applique l'inverse des changements précédents. C'est la bonne méthode pour un commit partagé sur GitHub, car elle évite de perturber l'historique des collaborateurs.
4) Quand on a du code non terminé en cours et qu'on doit basculer tout de suite sur une autre branche (par exemple pour corriger un bug urgent sur `main`), sans devoir faire un commit bâclé ou incomplet.
5) Quand une branche contient plusieurs expérimentations et qu'un seul commit nous intéresse (une correction urgente, par exemple). Utiliser `git cherry-pick` permet de récupérer seulement ce patch précis sans importer le reste de la branche de test sur `main`.
6) C'est le pointeur qui indique l'endroit exact où l'on se trouve dans l'historique. En général, il pointe vers la branche active, mais il peut pointer directement vers un commit précis si l'on navigue dans le passé (état detached HEAD).
7) Le commit situé deux crans avant le commit actuel (le grand-parent de HEAD). 
8) À marquer d'un nom fixe et immuable un commit important dans le temps (bonus du message du commit), la plupart du temps pour identifier une version stable comme v1.0.0.
9) ls rendent l'historique lisible et permettent de comprendre rapidement ce qui a été fait. Si un problème survient, on identifie beaucoup plus vite le commit en cause (avec `git bisect`), et on peut annuler ou extraire une modification précise (`revert` ou `cherry-pick`) sans toucher au reste du code.
10) D'une part pour la sécurité, afin de ne jamais exposer d'identifiants ou de clés secrètes stockés dans .env. D'autre part pour ne pas alourdir le dépôt avec des fichiers générés ou temporaires qu'on peut recréer localement, comme des logs (debug.log), du cache ou node_modules.
