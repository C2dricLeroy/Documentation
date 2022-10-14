# Linters and Formatters

### For what usage ? 

It exists differents ways of writing code. In a way to uniform code between developpers, companies began to develop some conventions. This conventions are used by teams for making their code intelligible and readable for all. 

Conventions covered differents domains: 

- Indentation style
- Conventions on how to name and how to structure your project's files.
- Commentaries and documentation of the source code
- Variable declaration

In this context, **linters** and **formatters** both tries to modify our source code in order to make it clean. 

Following this rules of convention gives lots of advantages like:

- A better software maintenance (40 to 80 % less cost of maintenance)
- Improve readabilty of code for other software engineers and make the process of _peer review_ easier.

The biggest tech compagnies developss their own conventions for Javascript writing: 

* **Standard Style Guide** : Contains a linter and a formatter, follow by Github, NPM, Heroku or MongoDB.
    - No configuration, easy to use. 
    - Automatically format your code.
        >https://github.com/standard/standard_

* **Google Style Guide** : Google also released a guide for javascript, but also for HTML / CSS / C++ / TypeScript or Angular. 
    - Used by Default in ESLint
    > https://google.github.io/styleguide/

* **Airbnb StyleGuide** : One of the most popular. From objects to performance testing. Offer conventions for CSS, JS, Ruby and React. It is appreciated for it :
    - Consistency
    - Readability
    - Predictability
    - Efficacity
    > https://github.com/airbnb/javascript

* **Clean Code Style Guide** : Taken from the book of Robert C. Martin, principles of this book have been taken and applied to JavaScript development. It is more like a list of good practices for a better readability of Javascript. 
    > https://github.com/ryanmcdermott/clean-code-javascript


### **_In this tutorial, we will follow the Airbnb Convention with a JavaScript stack._**

___

## Linters

### What is a linter? 

A linter is an automatic tool for code analysis. It analyses in live our code and warns us about errors. It runs **before** the compilation (or execution - according to your language). In this context, the linter is considered as a static tool.
Linter is often used with a **formatter** and other tools.
It exists three main ways of using a linter: With _command line interface_, in an _extension_ of your code editor, or in the process of _continuous integration_. This last option coupled to the formatter can automatically correct and format every new commit. 

It's not the same as the debugger and it can't replace it. 

_example :_
> _A servor-side script can't use the window object. It is possibl to configure the linter to prevent this kind of error._

### Difference between Linter and Debugger

The Debugger can also be considered as an error management tool, but it's **dynamic**! Debugger allows us to decompose the execution of our code and it helps us to detect dynamics errors: variable type, memory gestion, ...

### Existing linters

Today, there are different linter: 

* **JSLint**: 
* **JSHint**:
* **ESLint**: The most used and most known. It's a very versatile and configurable linter. It also contain a formatter. It can be integrated in your _continuous integration_

_These three linters also allows us to correct our code directly in our browsers, but we don't recommand this practic._

### Example with ESLint

#### Installation & Configuration

1) Create a directory for your project and configure your node environment. 
   > mkdir newProject   
     npm init -y

2) Install ESLint and the Airbnb configuration
   > npm i eslint eslint-config-airbnb-base eslint-plugin-import

note: It is also possible to proceed to a global installation of ESlint (add -g), but this installation is not recommanded by the ESLint official documentation: 
   > npm i eslint eslint-config-airbnb-base eslint-plugin-import -g

3) We haven't config yet our ESLint. Let's create our config file: 
   > touch .eslintrc   
     code .eslintrc

4) In the config file _.eslintrc_, insert the following script: 
   >  {  
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

5) Now that you have ESLint installed and configured, install the "ESLint" extension. Close and restart, your ESLint is now available! 

6) ESLint can also be used with CLI (_command line interface_): 
    With a global config: 
   > eslint index.js

    With a local config: 
   > npx eslint index.js


## Formatters 