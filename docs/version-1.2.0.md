# Version 1.2.0

## Objectifs

La version 1.2.0 va apporter les modifications suivantes :

- Qualimétrie du code
- Tri des personnages par nom ou date de modification

```mermaid
gitGraph
    checkout main
    commit tag: "v1.2.0"
    branch develop
    checkout develop
    branch feature-sonarcloud
    checkout feature-sonarcloud
    commit id: "workflow"
    checkout develop
    merge feature-sonarcloud
    branch feature-sort
    checkout feature-sort
    commit id: "sort-api"
    commit id: "sort-ui"
    checkout develop
    merge feature-sort
    branch release-1.2.0
    checkout release-1.2.0
    commit id: "1.2.0.rc1"
    commit id: "doc"
    commit id: "1.2.0"
    checkout main
    merge release-1.2.0
    commit tag: "v1.2.0"
    checkout develop
    merge main

```

## Qualimétrie du code

La qualité du code est un élément important dans le développement d'une application. Elle permet de s'assurer que le code est lisible, maintenable et évolutif. Elle permet aussi de s'assurer que le code est conforme aux bonnes pratiques de développement.

Il existe de nombreux outils pour mesurer la qualité du code. Dans le cadre de ce projet, nous allons utiliser [SonarCloud](https://sonarcloud.io/). SonarCloud est un service cloud qui permet d'analyser la qualité du code d'un projet. Il est gratuit pour les projets open source.

Afin de s'intégrer avec SonarCloud il faut au préalable se créer un compte sur [SonarCloud](https://sonarcloud.io/) avec un compte GitHub. Puis créer un projet sur SonarCloud en lui associant le repository GitHub.

### Intégration avec GitHub

Afin de pouvoir ajouter un **check status**, lors d'un Pull Request, sur la qualité de code, nous allons lancer les analyses sonarcloud depuis une github action.

Créer la branche `feature/sonarcloud` :

```bash
git switch develop
git pull
git switch -c feature/sonarcloud
```

Pour cela, nous allons créer un fichier `.github/workflows/quality.yml` avec le contenu suivant :

```yaml
name: Quality
on:
  push:
  pull_request:
jobs:
  sonarcloud:
    name: SonarCloud
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of analysis
      - uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'npm'
      - run: npm ci
      - run: npm run test:coverage
      - name: SonarCloud Scan
        uses: SonarSource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}  # Needed to get PR information, if any
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
      # Check the Quality Gate status.
      - name: SonarQube Quality Gate check
        id: sonarqube-quality-gate-check
        uses: sonarsource/sonarqube-quality-gate-action@master
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

Ce fichier définit une action `Quality` qui va être lancée à chaque `push` ou `pull_request`. Cette action va :

- récupérer le code source
- installer l'environnement node
- installer les dépendances
- lancer les tests unitaires avec la couverture de code
- lancer l'analyse sonarcloud
- vérifier que la qualité du code est bonne grâce à une **Quality Gate**

Cette action utilise 2 secrets :

- `GITHUB_TOKEN` : ce token est automatiquement créé par GitHub et permet d'accéder aux informations du repository
- `SONAR_TOKEN` : ce token est créé sur SonarCloud et permet d'accéder aux informations du projet

Afin de générer le token SonarCloud, il faut se rendre sur [SonarCloud](https://sonarcloud.io/) et aller dans `My Account` > `Security` > `Generate Tokens`. Il faut ensuite ajouter le token dans les secrets du repository GitHub.

Il faut aussi décocher la case `Automatic Analysis` dans `Administration` > `Analysis Method` sur SonarCloud.

### Configuration de SonarCloud

Afin de faire le lien entre projet GitHub et projet SonarCloud, il faut ajouter un fichier `sonar-project.properties` à la racine du projet avec le contenu suivant :

```properties
sonar.projectKey=nom-du-projet
sonar.organization=nom-de-compte-github

sonar.javascript.lcov.reportPaths=./coverage/lcov.info
sonar.coverage.exclusions=**/*.test.js
```

Ce fichier définit les propriétés du projet SonarCloud :

- `sonar.projectKey` : identifiant du projet SonarCloud
- `sonar.organization` : organisation SonarCloud
- `sonar.javascript.lcov.reportPaths` : chemin vers le fichier de couverture de code
- `sonar.coverage.exclusions` : fichiers à exclure de la couverture de code

Les informations `sonar.projectKey` et `sonar.organization` sont disponibles sur la page du projet SonarCloud dans la section **Information**.

Commiter et pusher les modifications :

```bash
git add .github/workflows/quality.yml
git add sonar-project.properties
git commit -m "Add sonarcloud analysis"
git push --set-upstream origin feature/sonarcloud
```

### Vérification de la qualité du code

A chaque push, une analyse de la qualité du code est lancée. Elle est visible dans l'onglet `Actions` du repository, si le code ne passe pas la **Quality Gate**, l'action est en erreur. Il faut alors corriger les problèmes de qualité du code. On peut aussi voir l'analyse sur SonarCloud.

Nous n'avons pas défini de **Quality Gate** personnalisée, nous utilisons donc la **Quality Gate** par défaut de SonarCloud. Il serait possible de définir une **Quality Gate** personnalisée, mais cela n'est pas nécessaire dans le cadre de ce projet.

La **Quality Gate** par défaut de SonarCloud possède les critères suivants :

- **Coverage** : 80%, il ne faut pas que la couverture de code soit inférieure à 80%
- **Duplicated Lines** : 3%, il ne faut pas que le code dupliqué soit supérieur à 3%, si l'on possède du code dupliqué, il faut le factoriser grâce à des fonctions.
- **Maintainability Rating** : A, il faut que la note de maintenabilité soit supérieure à A, si la note est inférieure à A, il faut améliorer la qualité du code. La note de maintenabilité est calculée à partir de la complexité du code, de la taille du code, etc...
- **Reliability Rating** : A, il faut que la note de fiabilité soit supérieure à A, si la note est inférieure à A, il faut améliorer la qualité du code. La note de fiabilité est calculée à partir de la présence de bugs, de la présence de code mort, etc...
- **Security Rating** : A, il faut que la note de sécurité soit supérieure à A, si la note est inférieure à A, il faut améliorer la qualité du code. La note de sécurité est calculée à partir de la présence de failles de sécurité, etc...
- **Security Hotspots Reviewed** : 0, il ne faut pas de failles de sécurité, si il y en a, il faut les corriger.

Si le code ne passe pas la **Quality Gate**, il faut corriger les problèmes de qualité du code. Il peut être nécessaire de modifier le code, d'ajouter des tests unitaires, de factoriser du code, etc...

Une fois l'action `Quality` passée une première fois, nous pouvons ajouter ce nouveau check status dans la protection des branches `main` et `develop`.

Nous avons maintenant des contrôles de qualité du code à chaque push et pull request. 

Faire le nécessaire pour merger la branche `feature/sonarcloud` dans `develop`(pull request, review, merge).

## Tri des personnages par nom ou date de modification

Créer la branche `feature/sort` :

```bash
git switch develop
git pull
git switch -c feature/sort
```

### Modification de l'UI

Modifier le fichier `src/pages/CharactersPage.js` pour ajouter les paramètres `orderBy` et `order` :

```javascript
import React, { useState } from 'react';
import { CharactersList } from "../components/CharactersList";
import { NumberOfCharacters } from "../components/NumberOfCharacters";

import { useLoaderData } from 'react-router';
import { useSearchParams } from 'react-router-dom';

const CharactersPage = () => {
    // change the title of the page
    document.title = "Marvel App";

    // retrieve the characters using the useLoaderData hook
    const characters = useLoaderData();

    // Get the search params from the URL
    let [searchParams, setSearchParams] = useSearchParams();

    // Get the order and orderBy from the search params or set the default values
    const [order, setOrder] = useState(searchParams.get('order') || 'asc')
    const [orderBy, setOrderBy] = useState(searchParams.get('orderBy') || 'name')

    // Update the search params when the order or orderBy state changes
    React.useEffect(() => {
        setSearchParams({ order, orderBy })
    }, [order, orderBy, setSearchParams])

    return (
        <>
            <h2>Marvel Characters</h2>
            {/* Sort by  */}
            <label htmlFor="sort">Sort by:</label>
            <select data-testid='orderBy' value={orderBy} onChange={(e) => setOrderBy(e.target.value)}>
                <option value="name">Name</option>
                <option value="modified">Modified</option>
            </select>   
            &nbsp;
            {/* Order */}
            <label htmlFor="order">Order:</label>
            <select data-testid='order' value={order} onChange={(e) => setOrder(e.target.value)}>
                <option value="asc">Ascending</option>
                <option value="desc">Descending</option>
            </select>         
            <CharactersList characters={characters} />
            <br />
            <NumberOfCharacters characters={characters} />
        </>
    );
};

export default CharactersPage;
```

On utilise le hook `useSearchParams` pour récupérer les paramètres de l'URL. 

Le hook `useSearchParams` retourne un tableau avec 2 éléments :

- le premier élément est un objet qui permet de récupérer les paramètres de l'URL
- le second élément est une fonction qui permet de mettre à jour les paramètres de l'URL

Ensuite le hook `useState` permet de gérer les paramètres `orderBy` et `order` en les stockant dans le state. 

On utilise le hook `useEffect` pour mettre à jour les paramètres de l'URL lorsque les paramètres `orderBy` et `order` changent.


Modifier le fichier de test `src/pages/CharactersPage.test.js` :

```javascript
import { render, screen } from '@testing-library/react';
import CharactersPage from './CharactersPage';
import { BrowserRouter, MemoryRouter } from 'react-router-dom';
import { act } from 'react-dom/test-utils';

const characters = [
    {
        id: "1",
        name: "Thor"
    }
];

// mock the useLoaderData hook, so that we can test the CharactersPage component
jest.mock('react-router', () => ({
    ...jest.requireActual('react-router'), // use actual for all non-hook parts
    useLoaderData: () => {
        return characters;
    },
}));

describe('CharactersPage', () => {

    test('render CharactersPage component with default order and orderBy', () => {
        // when

        // then
        render(
            <MemoryRouter initialEntries={[`/`]} >
                <CharactersPage />
            </MemoryRouter>
        );

        // expect the document title to be "Marvel App"
        expect(document.title).toBe('Marvel App');


        // expect the heading 'Marvel Characters' to be in the document
        const h2Element = screen.getByRole('heading', { level: 2, name: "Marvel Characters" });
        expect(h2Element).toBeInTheDocument();

        // expect the character Thor to be in the document
        const thorElement = screen.getByText(characters[0].name);
        expect(thorElement).toBeInTheDocument();

        // expect the number of characters to be in the document
        const numberOfCharactersElement = screen.getByText(`There is ${characters.length} character`);
        expect(numberOfCharactersElement).toBeInTheDocument();
    });

    test('render CharactersPage component with order and orderBy from search params', async () => {
        // when
        const order = 'desc';
        const orderBy = 'modified';

        // then
        render(
            <MemoryRouter initialEntries={[`/?order=${order}&orderBy=${orderBy}`]} >
                <CharactersPage />
            </MemoryRouter>
        );

        // expect the document title to be "Marvel App"
        expect(document.title).toBe('Marvel App');

        // expect the heading 'Marvel Characters' to be in the document
        const h2Element = screen.getByRole('heading', { level: 2, name: "Marvel Characters" });
        expect(h2Element).toBeInTheDocument();

        // expect the character Thor to be in the document
        const thorElement = screen.getByText(characters[0].name);
        expect(thorElement).toBeInTheDocument();

        // expect the number of characters to be in the document
        const numberOfCharactersElement = screen.getByText(`There is ${characters.length} character`);
        expect(numberOfCharactersElement).toBeInTheDocument();


        const orderSelect = screen.getByTestId('order');
        expect(orderSelect).toHaveValue(order);

        // expect the orderBy select to have the value from the search params
        const orderBySelect = screen.getByTestId('orderBy');
        expect(orderBySelect).toHaveValue(orderBy);
    });

    test('render CharactersPage component with order and orderBy when the select changes', async () => {
        // when
        const order = 'desc';
        const orderBy = 'modified';

        // then
        render(
            <MemoryRouter initialEntries={[`/`]} >
                <CharactersPage />
            </MemoryRouter>
        );

        // when
        await act(() => {
            // change the order select to desc
            const orderSelect = screen.getByTestId('order');
            orderSelect.value = order;
            orderSelect.dispatchEvent(new Event('change', { bubbles: true }));

            // then
            expect(orderSelect).toHaveValue(order);

            // change the orderBy select to modified
            const orderBySelect = screen.getByTestId('orderBy');
            orderBySelect.value = orderBy;
            orderBySelect.dispatchEvent(new Event('change', { bubbles: true }));

            // then
            expect(orderBySelect).toHaveValue(orderBy);
        });
    });
});
```

On utilise le composant `MemoryRouter` pour tester les paramètres de l'URL. Le composant `MemoryRouter` permet de simuler un router sans avoir besoin d'un navigateur. 

On utilise le composant `act` pour tester les changements de valeur des `select`, on simule ainsi une action de l'utilisateur.

On peut maintenant récupérer les paramètres `orderBy` et `order` dans l'URL et les utiliser pour trier les personnages.

Modifier le fichier `src/routes.js` pour ajouter les paramètres `orderBy` et `order` :

```javascript
import Layout from "./Layout";
import AboutPage from "./pages/AboutPage";
import ContactPage from "./pages/ContactPage";
import CharactersPage from "./pages/CharactersPage";

import CharacterDetailPage from "./pages/CharacterDetailPage";
import { getCharacterById, getCharacters } from "./api/character-api";

const routes = [
    {
        path: "/",
        element: <Layout />,
        children: [
            {
                path: "/",
                element: <CharactersPage />,
                loader: ({request}) => {
                    const url = new URL(request.url);
                    const orderBy = url.searchParams.get("orderBy");
                    const order = url.searchParams.get("order");

                    if (orderBy && order) {
                        return getCharacters(orderBy, order);
                    }else{
                        return getCharacters();
                    }
                },
            },
            {
                path: "/characters/:id",
                element: <CharacterDetailPage />,
                loader: ({ params }) => getCharacterById(params.id),
            },
            { 
                path: "/about", 
                element: <AboutPage /> 
            },
            { 
                path: "/contact", 
                element: <ContactPage /> 
            },
        ],
    },
];

export default routes;
```

On utilise le composant `URL` pour récupérer les paramètres `orderBy` et `order` de l'URL. On les passe ensuite à la fonction `getCharacters`.

### Modification de l'API

Modifier la fonction `getCharacters` du fichier `src/api.js` pour ajouter les paramètres `orderBy` et `order` :

```javascript
function getCharacters(orderBy = 'name', order = 'asc') {
  ...
}
```

Implémenter le tri, en fonction des paramètres `orderBy` et `order`, la méthode `sort` permet de trier un tableau grâce à une fonction de comparaison. La fonction de comparaison prend 2 paramètres et retourne un nombre négatif si le premier paramètre est inférieur au second, 0 si les 2 paramètres sont égaux et un nombre positif si le premier paramètre est supérieur au second.

Créer la pull request `feature/sort` afin de voir si le nouveau code passe bien les différents contrôles (tests unitaires, qualité du code)

Une fois la pull request validée, merger la branche `feature/sort` dans `develop`.

Puis faire le nécessaire pour créer la release `1.2.0` et valider la release.