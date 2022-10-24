- [Comment contribuer à un projet Opensource ?](#comment-contribuer-à-un-projet-opensource-)
  - [Définition des termes:](#définition-des-termes)
  - [Schéma:](#schéma)
  - [Les étapes essentielles :](#les-étapes-essentielles-)

# Comment contribuer à un projet Opensource ? 

Contribuer à un projet Opensource lorsque l'on est débutant peut se révêler une tâche ardue et rebutante. Pourtant, cet entraînement est indispensable afin de découvrir la méthode de travail avec Git qui sera plus tard utilisée en entreprise.  

Dans ce tutoriel, nous décidons d'utiliser Git flow afin de simplifier les commandes git utilisées. L'équivalence 

## Définition des termes: 

- Upstream : C'est le repository Github officiel du projet.
- Origin : C'est le repository Github utilisateur, créé après avoir effectuer la commande ```fork```sur le Upstream. 
- local : C'est un clone en version locale de 

## Schéma: 

## Les étapes essentielles : 

1) Sur Github, se rendre sur le repository officiel du projet auquel on souhaite contribuer, et le fork. Cette acton crée une copie du projet dans nos repository Github.  

2) Sur son ordinateur, clone le repository origin (présent sur nos repository Github)  

3) Entrer dans le clone du repository. Nous n'avons pas besoin de run la commande ```git init``` car nous sommes dores et déjà passés par Github, Git est donc déjà actif.  

4) Nous devons désormais définir notre Upstream. Cette commande permettra plus tard de se tenir au courant des éventuelles mises à jour. 
   > git remote add upstream \<lien vers repo\>  
5) Afin de tester la validité de notre poste de travail, nous pouvons exécuter la commande ```git pull upstream main```.  

6) Nous allons désormais utiliser Git flow afin d'initier notre projet. Cette commande crée deux branches: la branche ```main```et la branche ```develop```. Nous allons travailler sur la branche develop. Les réponses aux questions peuvent être blanches, appuyer sur Entrer.  
   > git flow init

7) La fonctionnalité que nous allons ajouter s'appelle une feature. Ajouter une fonctionnalité avec git flow crée une branche pour le nom de cette fonctionnalité spécifique.  
   > git flow feature start \<feature\>   
Cette commande corresponds aux deux commandes git suivantes ```git checkout develop``` et ```git checkout -b feature/<...>```

8) Travailler votre code ! N'oubliez pas, il faudra ajouter votre travail puis le commit, la commande ```git status```peut vous être utile pour savoir où vous en êtes.  
   > git add \<fichier\>  
   > git commit -m "my message"  

9) Notre fonctionnalité étant enregistrée avec le commit, nous pouvons clore notre feature.  
   > git flow feature finish \<feature\>  
Cette commande correspond aux commandes Git ```git checkout develop```, ```git merge feature/<...>``` et ```git branch -D feature/<...>```.   

10) Il faut désormais s'assurer que durant notre travail, le repository officiel n'a pas été modifié et que ces modifications n'interfèrent pas avec notre travail.   
   > git pull upstream main
   > git pull upstream develop   

11) Une fois l'entièreté du projet à jour, il est possible de push son travail sur le repository origin.   
   > git push -u origin develop  

12) Vous pouvez désormais vous rendre sur Github, la branche ```Develop``` devrait être en avant du nombre de commit effectué par rapport à la branche Develop du repository Upstream. La Pull Request vous permet d'envoyer votre modification au propriétaire du repository Upstream et aux différents reviewers. 

