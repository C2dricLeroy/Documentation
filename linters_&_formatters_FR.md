# Les linters et formatters 

### Dans quel but ? 

Il existe plusieurs façons d'écrire un même code. De façon à uniformiser le code de différents développeurs dans les entreprises, des **conventions** existent. Ces conventions permettent aux développeurs d'une équipe de rendre un code uniformisé, compréhensible par tous. 

Les conventions couvrent différents domaines :

- Style d'indentation
- convention de nommage et d'organisation des fichiers (architecture projet)
- commentaire et documentation du code source 
- déclaration des variables

Dans ce cadre, les **linter** et **formatter** permettent de "modifier" un code source afin d'en rendre une version claire.

Suivre ces règles de convention apporte différents avantages : 

- Une meilleure maintenance logicielle (40 à 80% de réduction du coût de maintenance)
- Améliore la readabilité du code pour d'autres ingénieurs logiciel et rends plus facile le peer review. 

<br/>

Les plus grandes compagnies ont sorties leurs conventions respectives concernant Javascript:

* **Standard Style Guide** : Contient un linter et un formatter, suivi par Github, NPM, Heroku, MongoDB.
    - Pas de configuration, simple à utiliser et suivre.
    - Formatte automatiquement le code
    >https://github.com/standard/standard_

* **Google Style Guide** : Google a sorti un guide pour Javascript, mais également pour HTML / CSS / C++ / TypeScript ou Angular. 
    - Fourni avec ESLint 
   > https://google.github.io/styleguide/

* **Airbnb Style Guide**: Un des plus populaire. Très complet, des objets au testing. Propose des conventions CSS, JS, Ruby et React. Il est apprécié pour sa :
    - Consistence
    - Readabilité
    - Prédictabilité
    - Efficacité 
     
    > https://github.com/airbnb/javascript

* **Clean Code Style Guide**: Tiré du livre de Robert C. Martin, les principes de ce livre ont été repris et appliqués au Javascript. C'est une liste de bonnes pratiques pour une écriture lisible du JavaScript. 
    >     >https://github.com/ryanmcdermott/clean-code-javascript
https://github.com/ryanmcdermott/clean-code-javascript


#### **_Nous faisons le choix de suivre la convention proposée par AirBnb dans une stack JavaScript._**

<br/>

_ _ _


<br/>


## Les linters 

### Qu'est-ce qu'un linter ? 

Le linter est un outil automatisé d'analyse de code. Il analyse en temps réel notre code et prévient des erreurs, pour cela, il s'éxecute **avant** que le code ne soit compilé (ou exécuté - selon le langage utilisé). Le linter est donc un outil d'analyse **statique** du code. Il existe trois majeures façons d'utiliser un linter: En _ligne de commande_, dans une _extension_ de l'éditeur de code, ou dans le processus de _développement continu_. Cette dernière option permet à chaque commit d'être corrigé et formatté. 
Le linter est souvent utilisé en parralèle d'un **formatter** et d'autres outils. C'est un outil différent qui ne remplace pas le débuggeur. 

_exemple:_ 
> _Un script déstiné à tourner sur serveur ne doit pas contenir l'objet window. Il est possible de configurer le linter pour nous prévenir de cette erreur._ 

<br/>

### Différence avec un débugger

Le débuggeur peut également être considéré comme un outil de gestion des erreurs, cependant, c'est un outil **dynamique**! Le débuggeur permet donc de décomposer l'éxecution du code afin de détecter des erreurs dynamiques : type des variables, gestion de mémoire, ... 

<br/>

### Les linters existants 

Il existe différents linter: 

* **JSLint** est un linter connu... Il ne permet pas beaucoup de configuration. 
* **JSHInt** Permet plus de configurations
* **ESLint** est le plus connu et le plus utilisé. C'est un linter extrêmement configurable qui possède également en son sein un formatter. Il peut de plus s'intégrer au processus de développement continu.

_Ces trois linters proposent une alternative de correction du code directement sur navigateur, nous ne recommandons pas cette pratique aux développeurs._ 

<br/>

## Exemple avec ESLint

### Installation et configuration : Projet vs. Global

1) Créer un dossier projet, puis y adjoindre un environnement node. 
   > mkdir newProject  
    npm init -y

2) Installer Eslint avec sa configuration Airbnb
   > npm i eslint eslint-config-airbnb-base eslint-plugin-import

note: Il est également possible d'installer ESlint en global avec cette commande (ajout du -g), mais cette installation est déconseillée par la documentation officielle Eslint :  
   > npm i eslint eslint-config-airbnb-base eslint-plugin-import -g

3) En l'absence de configuration officielle lors de l'installation d'EsLint, il est important de créer son fichier de configuration. 
   > touch .eslintrc  
     code .eslintr

4) Dans le fichier de configuration, insérer la configuration suivante: 

   > {  
  "extends": ["airbnb-base"],  
  "env": {  
    "node": true,  
    "es6": true,  
    "browser": true  
  },  
  "rules": {  
    "no-console": "off"  
  }  
}  

5) Installer l'extension "Eslint" sur votre éditeur de code favori. Fermer puis relancer, votre Eslint est maintenant disponible! 

6) Il est également possible d'utiliser Eslint en ligne de commande directement depuis votre terminal: 
    Pour une installation globale: 
> eslint index.js  

    Pour une installation locale: 
> npx eslint index.js  

<br/>

### Incorporation dans le processus d'intégration continue: 


_ATTENTION: Ce tutoriel est écrit dans le cadre d'un projet Gitlab, Gitlab étant particulièrement permissif dans les outils Devops proposés._

1) Ouvrir les **_settings_** de votre projet, puis aller dans **_CI/CD_**, puis **_runners_**
 > Vous devriez voir apparaitre deux colonnes: **Shared** runners et **Specific** runners

2) Les runners sont des machines virtuelles permettant d'executer une image de notre application sous docker. Le fichier de configuration _.gitlab-ci.yml_ permet de spécifier: 
   - Quelle image utiliser?
   - Quel script exécuter ? 
   - Quelles dépendances installer ? 

  > touch .gitlab-ci.yml

3) Remplir le fichier de configuration : 
  > image: node  
    stage:  
    \# I just want to lint, so I will create a "lint" stage  
    \- lint  
    \# Lets name our Job eslint, because that's what it's doing.  
    eslint:  
    \# tell eslint what stage it is. (This could also be build or test for example)
    stage: lint   
    \# What scripts do we want to run?  
    script:  
    # install eslint  
    - npm i eslint  
    # Run eslint  
    - node_modules/eslint/bin/eslint.js  

4) Commit et push le fichier. 

5) Pour voir le linter en action, aller dans _jobs_

6) Pour aller plus loin: De nouveau, le fichier de configuration permet de configurer la convention choisie, il suffit dans le script de préciser les configurations souhaitées. Si il y en a plusieurs, séparer par le caractère "\" (_backslah_)

  > script:   
    \# Install eslint   
    - |    
    npm install eslint \   
    eslint-config-airbnb \   
    eslint-config-prettier \   
    eslint-plugin-flowtype \ # Any ideas on what I might want to do next?   
    eslint-plugin-import \   
    eslint-plugin-jsx-a11y \   
    eslint-plugin-prettier \   
    eslint-plugin-react   

<br/>

_ _ _ 


<br/>

## Les formatteurs

### Qu'est-ce qu'un formatter et pouquoi l'utiliser? 

Toujours dans l'optique de suivre des conventions données, le **formatteur** permet une retouche du code original afin que le code sortant correspond à un style consistent. 

En d'autres termes, si le linter analyse statiquement l'_intérieur_ de notre code, le formatter au contraire prends en charge l'_extérieur_, soit la partie visuelle.  

Utiliser donc le **formatteur** pour votre style et le **linter** pour vos bugs! 

Example: 

Une fonction peut être déclarée de la façon suivante: 
  > function init({ option1, option2, option3, option4, option5, option6, option7 }) {  
    //...   
    }   

Un formatter sortira le code source donné en modifiant son aspect visuel, son style: indentation, espaces, ...
  > funtion init ({   
      option1,   
      option2,    
      option3,   
      option4,   
      option5,   
      option6,   
      option7   
    })   

<br/>


### Comment l'utiliser? L'exemple de Prettier
 
**Prettier** peut être utilisé de différentes manières : 

1) La plus simple: L'extension VSCode. 

  - Commencer par installer l'extension VSCode "Prettier"
  - Utiliser la combinaison de touche "Ctrl + Shift + I"
  - Votre fichier se formatte automatiquement selon la configuration Prettier! 

_Note: Il est possible dans les settings de configurer l'extension, ou de de créer un fichier de configuration._  


2) La _command line interface_:  


  - Commencer par installer prettier dans l'environnement node choisi OU globalement (ajout du _-g_ en fin de commande):
  A la racine du dossier projet: 
  > npm init -y
  > npm install --save-dev --save-exact prettier
  - Utiliser la commande pour formatter le code, l'output sort formatté! 
   Si installation globale:
  > prettier index.js
   Si installation locale: 
  >npx prettier index.js

  - Autre option utile, si vous souhaitez que le formattage s'effectue directement dans le fichier, ajouter _--write_ 
  > npx prettier index.js --write

  - Pour formatter tous les fichiers du projet pris en charge par prettier, ne pas spécifier de fichier: 
  > npx prettier --write

  - Il est possible de créer un fichier _.prettierignore_ afin d'y spécifier les éléments qui ne doivent pas être formattés.

  - Le drapeau _--check_ en commande produit un message lisible par l'utilisateur afin d'informer de l'état des fichiers: 
  > npx prettier --ckeck 

  - Le drapeau _--debug-check_ permet d'activer un "débuggeur" pour le formattage du code, ce drapeau ne peut être utilisé avec _write_. 

  - Le drapeau _--no-config_ permet d'utiliser la configuration Prettier par défaut.

  - De nombreux autres drapeaux sont disponibles en source [1]

<br/>

### Configurer Prettier : 

_Dans cet exemple, nous suivons la convention proposée par airbnb_

I) Installation globale et locale en CLI: 

De la même façon qu'il est possible de configurer ESLint de façon à suivre la convention Airbnb, il est possible de configurer Prettier au moyen du fichier _.prettierrc_

Dans le fichier _.prettierrc_ (si non existant, le créer), coller: 
> {  
  "semi": false,  
  "tabWidth": 2,  
  "singleQuote": true  
  }  

II) Configurer l'extension VScode: 

- Cocher la case "Prettier : semi"
- Cocher la case "Single Quote"
- Dans "Prettier: Tab Width", renseigner la valeur 2.

- Il est également possible d'accéder au ficher global de configuration avec la commande : 
> code . /home/$USER/prettierrc.json
Puis de coller le code suivant: 
> {  
  "semi": false,  
  "tabWidth": 2,  
  "singleQuote": true  
  }  

<br/>

## Conclusion

Vous devriez maintenant être en capacité, selon votre type d'installation favori, d'installer l'outil souhaité et de le configurer selon la convention choisie par votre équipe! 

sources: 
> https://en.wikipedia.org/wiki/Coding_conventions#Coding_conventions_for_languages  
  https://code-garage.fr/blog/guides-de-style-pour-javascript-incluant-google-github-airbnb/  
  https://enlear.academy/5-best-javascript-style-guides-640485e7b630  
  https://mindsers.blog/fr/post/linting-good-practices/   
  https://medium.com/medvine/install-eslint-global-with-airbnb-style-guide-and-use-it-in-vscode-d752dfa40b21     
  https://eslint.org/docs/latest/user-guide/getting-started   
  https://prettier.io/docs/en/configuration.html    
  https://www.digitalocean.com/community/tutorialshow-to-format-code-with-prettier-in-visual-studio-code   
  https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode  
  https://www.codereadability.com/automated-code-formatting-with-prettier/  
  [1] https://runebook.dev/fr/docs/prettier/cli


  

