Dans cette première version, nous allons implémenter les fonctionnalités suivantes :

- Utilisation de git pour gérer l'historique des modifications du projet
- Utilisation de npm pour gérer les dépendances du projet
- Implémentation d'une page web avec HTML, CSS et JavaScript
    - Contenu statique de la page HTML (**H**yper**T**ext **M**arkup **L**anguage)
    - Application du style avec CSS (**C**ascading **S**tyle **S**heets)
    - Ajout d'interactivité avec **J**ava**S**cript pour afficher les personnages de Marvel

## 0. Prérequis

### 0.1. Installation de Node.js

Node.js est un environnement d'exécution JavaScript. Il permet d'exécuter du code JavaScript en dehors d'un navigateur web. Il est basé sur le moteur JavaScript V8 de Google, qui est le moteur JavaScript utilisé par le navigateur Chrome.

Pour installer Node.js, rendez-vous sur le site officiel : https://nodejs.org/en/

Dans un premier temps, nous allons utiliser Node.js pour installer des dépendances, qui sont des bibliothèques JavaScript. La première dépendance que nous allons installer nous permettra de créer un serveur web local.

Nous irons plus loin avec Node.js plus tard, pour utiliser des librairies JavaScript telles que React, qui est une librairie JavaScript développée par Facebook, qui permet de créer des interfaces utilisateur.

### 0.2. Installation de Visual Studio Code

Visual Studio Code est un éditeur de code open source, développé par Microsoft. Il est disponible pour Windows, Mac et Linux.

Pour installer Visual Studio Code, rendez-vous sur le site officiel : https://code.visualstudio.com/

Visual Studio Code est un éditeur de code très complet, qui permet de développer dans de nombreux langages de programmation. Il est très utilisé par les développeurs JavaScript, car il permet d'installer des extensions pour améliorer l'expérience de développement. Nous verrons plus tard comment installer des extensions pour Visual Studio Code.

### 0.3. Installation de Git

Git est un logiciel de gestion de versions décentralisé. Il permet de gérer l'historique des modifications d'un projet. Il est utilisé par GitHub, qui est un service web d'hébergement et de gestion de code source.

Pour installer Git, rendez-vous sur le site officiel : https://git-scm.com/

Nous verrons plus tard comment utiliser Git pour gérer l'historique des modifications de notre projet.

Il est toutefois nécessaire d'appliquer quelques configurations avant de pouvoir utiliser Git, voir [Configurer Git](https://but-sd.github.io/memo-git/configurer-git/){:target="_blank"}.

## 1. Initialisation du projet

### 1.1. Création du projet sur GitHub

Créer un nouveau projet sur GitHub avec le nom `marvel-app`. Cocher la case `Initialize this repository with a README`.

Cela va créer un nouveau dépôt de code sur GitHub, avec un fichier README.md. Le fichier README.md est un fichier au format Markdown, qui permet de documenter le projet. Nous allons l'utiliser pour expliquer comment installer et utiliser le projet. Nous verrons plus tard comment utiliser Markdown.

### 1.2. Clonage du projet

Cloner le projet sur votre ordinateur avec la commande suivante :

```bash
git clone url-du-projet
```

### 1.3. Initialisation du projet avec npm

Créer un nouveau projet avec la commande suivante :

```bash
npm init -y
```

Cela va créer un nouveau fichier `package.json` à la racine du projet. Ce fichier contient les informations du projet, ainsi que la liste des dépendances du projet.

### 1.4. Installation des dépendances

Installer les dépendances suivantes :

```bash
npm install --save-dev browser-sync
```

`browser-sync` est une dépendance qui permet de créer un serveur web local, avec un rechargement automatique du navigateur à chaque modification du code source. Cela nous permettra de tester simplement la première version de notre application en local.

### 1.3. Configuration de browser-sync

Créer un fichier `bs-config.js` à la racine du projet avec le contenu suivant :

```javascript
module.exports = {
    files: [
        'src/**/*.{html,htm,css,js}'
    ],
    server: {
        baseDir: './src'
    }
};
```

Ce fichier permet de configurer browser-sync. Nous indiquons que nous souhaitons surveiller les fichiers html, css et js dans le dossier `src`, et que le serveur web doit servir les fichiers du dossier `src`.

### 1.4. Ajout de scripts npm

Modifier le fichier `package.json` pour ajouter les scripts suivants :

```json
{
    "scripts": {
        "start": "browser-sync start --config bs-config.js"
    }
}
```

Cela nous permettra de lancer le serveur web local avec la commande suivante :

```bash
npm start
```

### 1.5. Création du dossier `src`

Créer un dossier `src` à la racine du projet. Ce dossier contiendra le code source de notre application.

Ajouter un fichier `index.html` dans le dossier `src` avec le contenu suivant :

````html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>Hello, World!</title>
    </head>
    <body>
        <h1>Hello, World!</h1>
    </body>
</html>
````

Lancer le serveur web local avec la commande suivante :

```bash
npm start
```

Ouvrir l'adresse http://localhost:3000 dans un navigateur web. Vous devriez voir le contenu du fichier `index.html`.

## 2. Ajout de contenu statique

### 2.1. Ajout de contenu HTML

Modifier le fichier `index.html` pour mettre le contenu suivant :

```html
<!DOCTYPE html>
<html lang="fr">
    <head>
        <meta charset="utf-8">
        <title>Marvel App</title>
    </head>
    <body>
        <h1>Marvel App</h1>
    </body>
</html>
```

### 2.2. Ajout de contenu CSS

Créer un fichier `style.css` dans le dossier `src` avec le contenu suivant :

```css
body {
    font-family: sans-serif;
    margin: 0;
    padding: 0;
}

```

Modifier le fichier `index.html` pour ajouter le lien vers le fichier `style.css` :

```html
<!DOCTYPE html>
<html lang="fr">
    <head>
        <meta charset="utf-8">
        <title>Marvel App</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>Marvel App</h1>
    </body>
</html>
```

L'attribut `rel` permet d'indiquer le type de lien. Ici, nous indiquons que le lien est une feuille de style. L'attribut `href` permet d'indiquer l'adresse du fichier.

L'apparence de la page web devrait changer. Nous avons appliqué un style par défaut au corps de la page web, pour supprimer les marges et les espacements par défaut.

### 2.3. Ajout de contenu JavaScript

Créer un fichier `script.js` dans le dossier `src` avec le contenu suivant :

```javascript
console.log("Welcome to marvel app");
```

Modifier le fichier `index.html` pour ajouter le lien vers le fichier `script.js` :

```html
<!DOCTYPE html>

<html lang="fr">
    <head>
        <meta charset="utf-8">
        <title>Marvel App</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>Marvel App</h1>
        <script src="script.js"></script>
    </body>
</html>
```

L'attribut `src` permet d'indiquer l'adresse du fichier.

Ouvrir la console du navigateur web. Dans Chrome, vous pouvez ouvrir la console avec le raccourci `Ctrl + Maj + J`. Vous devriez voir le message `Welcome to marvel app`.

## 3. Ajout de contenu dynamique

### 3.1. Récupération des données

Dans un premier temps, nous allons simuler un appel d'API pour récupérer des données. Nous verrons plus tard comment appeler une API. Pour cela nous allons charger les données depuis un fichier JSON (JavaScript Object Notation).

Créer un dossier `src/data` à la racine du projet. Dans ce dossier ajouter le fichier `characters.json` avec le contenu suivant :

```javascript

[
    {
        "name": "Beast"
    },
    {
        "name": "Captain America"
    },
    {
        "name": "Deadpool"
    },
    {
        "name": "Groot"
    },
    {
        "name": "Hulk"
    },
    {
        "name": "Iron Man"
    },
    {
        "name": "Rocket Raccoon"
    },
    {
        "name": "Silver Surfer"
    },
    {
        "name": "Thanos"
    },
    {
        "name": "Thor"
    },
    {
        "name": "Wolverine"
    }
]

```

Pour récupérer les données depuis le fichier JSON, nous allons utiliser la fonction `fetch` de JavaScript. Cette fonction permet de faire des requêtes HTTP. 

Ajouter le code suivant dans le fichier `script.js` :

```javascript
console.log("Welcome to marvel app");

/**
 * Get characters from json file 
 */
const getCharacters = () => {
    const API_URL = 'http://localhost:3000/data/characters.json';
    return fetch(API_URL)
        .then(response => response.json());
};

// Call getCharacters function, and log the result
// get characters is a async function, so we need to use then
const characters = getCharacters().then(characters => {
    console.log(characters);
});

```

La fonction `fetch` retourne une promesse. Une promesse est un objet qui représente une valeur qui peut être disponible maintenant, dans le futur, ou jamais. Une promesse peut être dans l'un des états suivants :

- `pending` : la promesse n'est pas encore résolue
- `fulfilled` : la promesse est résolue
- `rejected` : la promesse est rejetée

Pour récupérer la valeur d'une promesse, nous pouvons utiliser la méthode `then`. Cette méthode prend en paramètre une fonction qui sera appelée lorsque la promesse sera résolue. Cette fonction prend en paramètre la valeur de la promesse.

Pour récupérer les personnages, nous devons appeler la fonction `getCharacters`, puis utiliser la méthode `then` pour récupérer les personnages. Nous pouvons ensuite utiliser la méthode `then` pour afficher les personnages dans la console.

Ouvrir la console du navigateur web. Vous devriez voir le tableau des personnages.

### 3.2. Affichage des personnages

Modifier le fichier `index.html` pour ajouter une liste de personnages :

```html
<!DOCTYPE html>

<html lang="fr">
    <head>
        <meta charset="utf-8">
        <title>Marvel App</title>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <h1>Marvel App</h1>
        <ul id="characters"></ul>
        <script src="script.js"></script>
    </body>

</html>

```

Modifier le fichier `script.js` pour afficher les personnages dans la liste :

```javascript

console.log("Welcome to marvel app");

/**
 * Get characters from json file 
 */
const getCharacters = () => {
    const API_URL = 'http://localhost:3000/data/characters.json';
    return fetch(API_URL)
        .then(response => response.json());

};

// Call getCharacters function, and add characters to the list
const characters = getCharacters().then(characters => {
    const charactersList = document.getElementById('characters');
    characters.forEach(character => {
        const characterElement = document.createElement('li');
        characterElement.textContent = character.name;
        charactersList.appendChild(characterElement);
    });
});

```

Nous avons ajouté une liste de personnages dans le fichier `index.html`. Nous avons ajouté un identifiant `characters` à la liste. Cela nous permettra de récupérer la liste dans le fichier `script.js`.

Nous avons ensuite récupéré la liste des personnages dans le fichier `script.js`. Nous avons parcouru la liste des personnages, et pour chaque personnage nous avons créé un élément `li` et nous l'avons ajouté à la liste.

## 4. Commit et push des modifications

Afin de sauvegarder nos modifications, nous allons pousser les modifications sur GitHub. Nous verrons plus tard comment fonctionne Git.

### 4.1. Commit des modifications

Créer un fichier `.gitignore` à la racine du projet avec le contenu suivant :

```
node_modules
```

Ce fichier permet d'ignorer le dossier `node_modules`, qui contient les dépendances du projet. Nous n'avons pas besoin de sauvegarder les dépendances du projet, car elles peuvent être installées à partir du fichier `package.json`.

Ajouter les modifications au prochain commit avec la commande suivante :

```bash
git add .
```

Créer un commit avec la commande suivante :

```bash
git commit -m "Add static and dynamic content"
```

### 4.2. Push des modifications

Envoyer les modifications sur GitHub avec la commande suivante :

```bash
git push
```
