# Version 1.3.0

## Objectifs

- Amélioration du code
    - Correction des éventuelles `Bugs` et `Code Smells` identifiés par SonarQube
    - Amélioration de la couverture de test
- Création d'un pie chart pour visualiser les capacités des personnages
    - Implémentation avec la librairie `d3.js`
    - Implémentation avec la librairie `recharts`

## Amélioration du code

**Bug et Code Smells**

Corriger les éventuelles `Bugs` et `Code Smells` identifiés par SonarQube. Sonarqube explique comment corriger une issue dans l'onglet `How can I fix it ?`. github copilot peut vous aider dans cette tâche, attention toutefois de vérifier le code généré par github copilot, il peut être incomplet ou incorrect.

Afin de corriger l'issue `Refactor the redundant 'await' on a non-promise` pour le fichier `src/App.test.js` appliquer la solution suivante:

```javascript
import { render, screen } from '@testing-library/react';
import App from './App';
import { act } from 'react-dom/test-utils';

test('render Marvel App', async () => {
  await act(async() => {
    render(<App />);
  });

  const h1Element = screen.getByRole('heading', { level: 1, name: "Marvel App" });
  expect(h1Element).toBeInTheDocument();
});

```

Le mot clé `async` est ajouté à la fonction `act` afin de rendre la fonction `test` asynchrone. 

**Couverture de test**

Améliorer la couverture de test, github copilot peut vous aider à écrire les tests manquants (bouton droit sur le fichier puis `Copilot / Generate tests`). Comme pour les `Bugs` et `Code Smells` identifiés par SonarQube, attention à bien vérifier le code généré par github copilot et à le modifier afin d'ajouter les vérifications nécessaires.

## Visualisation des données 

Modifier le fichier `src/data/characters.json` afin d'ajouter des données sur les capacités des personnages.

```javasript
[
    {
        "id": "1009175",
        "name": "Beast",
        "description": "",
        "modified": "2014-01-13T14:48:32-0500",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/2/80/511a79a0451a3",
            "extension": "jpg"
        },
        "capacities": {
            "force": 5,
            "intelligence": 8,
            "durability": 6,
            "energy": 6,
            "speed": 1,
            "fighting": 3
        }
    },
    {
        "id": "1009220",
        "name": "Captain America",
        "description": "Vowing to serve his country any way he could, young Steve Rogers took the super soldier serum to become America's one-man army. Fighting for the red, white and blue for over 60 years, Captain America is the living, breathing symbol of freedom and liberty.",
        "modified": "2020-04-04T19:01:59-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/3/50/537ba56d31087",
            "extension": "jpg"
        },
        "capacities": {
            "force": 4,
            "intelligence": 3,
            "durability": 3,
            "energy": 1,
            "speed": 2
        }
    },
    {
        "id": "1009268",
        "name": "Deadpool",
        "modified": "2020-04-04T19:02:15-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/9/90/5261a86cacb99",
            "extension": "jpg"
        },
        "capacities": {
            "force": 4,
            "intelligence": 3,
            "durability": 2,
            "energy": 1,
            "speed": 2
        }
    },
    {
        "id": "1010743",
        "name": "Groot",
        "description": "",
        "modified": "2013-10-17T15:01:37-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/3/10/526033c8b474a",
            "extension": "jpg"
        },
        "capacities": {
            "force": 6,
            "intelligence": 1,
            "durability": 7,
            "energy": 1,
            "speed": 1
        }
    },
    {
        "id": "1009351",
        "name": "Hulk",
        "description": "Caught in a gamma bomb explosion while trying to save the life of a teenager, Dr. Bruce Banner was transformed into the incredibly powerful creature called the Hulk. An all too often misunderstood hero, the angrier the Hulk gets, the stronger the Hulk gets.",
        "modified": "2020-07-21T10:35:15-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/5/a0/538615ca33ab0",
            "extension": "jpg"
        },
        "capacities": {
            "force": 7,
            "intelligence": 6,
            "durability": 7,
            "energy": 1,
            "speed": 3
        }
    },
    {
        "id": "1009368",
        "name": "Iron Man",
        "description": "Wounded, captured and forced to build a weapon by his enemies, billionaire industrialist Tony Stark instead created an advanced suit of armor to save his life and escape captivity. Now with a new outlook on life, Tony uses his money and intelligence to make the world a safer, better place as Iron Man.",
        "modified": "2016-09-28T12:08:19-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/9/c0/527bb7b37ff55",
            "extension": "jpg"
        },
        "capacities": {
            "force": 6,
            "intelligence": 6,
            "durability": 6,
            "energy": 6,
            "speed": 5
        }
    },
    {
        "id": "1010744",
        "name": "Rocket Raccoon",
        "description": "A genetically-engineered alien with a knack for big guns and fast ships, Rocket serves as the backbone of the Guardians of the Galaxy!",
        "modified": "2014-07-17T17:32:43-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/9/b0/50fec1e49298a",
            "extension": "jpg"
        },
        "capacities": {
            "force": 2,
            "intelligence": 2,
            "durability": 2,
            "energy": 1,
            "speed": 2
        }
    },
    {
        "id": "1009592",
        "name": "Silver Surfer",
        "description": "When Zenn-La was threatened by the world-devouring entity known as Galactus, Norrin Radd stood up for his home planet and offered to work for Galactus, finding him new planets to eat, in exchange for saving his own. Years later, the Surfer has protected Earth and many other planets, becoming one of the greatest heroes in the universe.",
        "modified": "2013-11-07T10:48:53-0500",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/3/50/527bb6490a176",
            "extension": "jpg"
        },
        "capacities": {
            "force": 6,
            "intelligence": 4,
            "durability": 7,
            "energy": 7,
            "speed": 7
        }
    },
    {
        "id": "1009697",
        "name": "Thanos",
        "modified": "2016-05-05T15:35:19-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/6/40/5274137e3e2cd",
            "extension": "jpg"
        },
        "capacities": {
            "force": 7,
            "intelligence": 6,
            "durability": 6,
            "energy": 7,
            "speed": 6
        }
    },
    {
        "id": "1009663",
        "name": "Thor",
        "modified": "2020-03-11T10:18:57-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/d/d0/5269657a74350",
            "extension": "jpg"
        },
        "capacities": {
            "force": 7,
            "intelligence": 2,
            "durability": 7,
            "energy": 6,
            "speed": 7
        }
    },
    {
        "id": "1009718",
        "name": "Wolverine",
        "modified": "2016-05-02T12:21:44-0400",
        "thumbnail": {
            "path": "http://i.annihil.us/u/prod/marvel/i/mg/2/60/537bcaef0f6cf",
            "extension": "jpg"
        },
        "capacities": {
            "force": 4,
            "intelligence": 2,
            "durability": 4,
            "energy": 1,
            "speed": 2
        }
    }
]
```

### `d3.js`

`d3.js` est une librairie JavaScript qui permet de manipuler le DOM pour créer des visualisations de données. Elle est très utilisée dans le monde du web pour créer des graphiques, des cartes, des diagrammes, etc.

Installer `d3.js` avec `npm`:

```bash
npm install d3
```

S'inspirer de [https://d3-graph-gallery.com/graph/donut_label.html](https://d3-graph-gallery.com/graph/donut_label.html){target="_blank"} pour générer un pie chart avec les capacités des personnages.

Créer le composant `src/components/D3PieChart.js` et implémenter le graphique avec `d3.js`.

```javascript
import { useEffect } from "react";
import * as d3 from "d3";

const drawChart = (data = []) => {
    // Mettre ici le code pour dessiner le graphique et le rattacher à la div avec l'id pie-container
};

export default function D3PieChart({
    data,
}) {
    // useEffect est un hook qui permet d'exécuter du code lorsque les données sont chargées
    useEffect(() => {
        let transformData = []

        // Transformer les données pour les mettre dans le format attendu par d3.js
        ...

        // draw the chart
        drawChart(transformData);
    }, [data]);

    return (
        // div qui contiendra le graphique
        <div id="pie-container" />
    );
}
```

Le composant `D3PieChart` génère une div avec l'id `pie-container` qui sera utilisée pour afficher le graphique. Le hook `useEffect` permet de lancer le code de la fonction `drawChart` uniquement lorsque les données sont chargées. 

La fonction `drawChart` permet de dessiner le graphique. Elle prend en paramètre les données à afficher. Elle utilise la librairie `d3.js` pour dessiner le graphique. Il n'y a pas de spécificité React dans cette fonction.

La documentation de `d3.js` est disponible à l'adresse [https://d3js.org/](https://d3js.org/).

Committer et pusher les modifications.

Ajouter le test unitaire pour le composant `D3PieChart` dans le fichier `src/components/D3PieChart.test.js`, github copilot peut vous aider à écrire le test (bouton droit sur le composant `D3PieChart` puis `Copilot / Generate tests`). 

Attention à bien vérifier le test généré par github copilot et à le modifier afin d'ajouter les vérifications nécessaires. Par exemple pour ce type de composant, on peut vérifier :

- que le svg est bien dessiné
- que les labels sont bien dessinés
- qu'il y a bien 6 arcs

### recharts

`Recharts` est une librairie React qui permet de créer des graphiques. Elle est basée sur `d3.js`. Elle permet de créer des graphiques manipulant des composants React. Cela peut être plus simple à utiliser que `d3.js` pour des développeurs React, mais elle est moins flexible que `d3.js`. 

Installer `recharts` avec `npm`:

```bash
npm install recharts
```

S'inspirer de [https://recharts.org/en-US/examples/PieChartWithPaddingAngle](https://recharts.org/en-US/examples/PieChartWithPaddingAngle){target="_blank"} pour générer un pie chart, `src/components/RechartsPieChart.js` avec les capacités des personnages.

***CharacterDetailPage***

Modifier le composant `src/pages/CharacterDetailPage.js` afin d'ajouter le pie chart généré avec `d3.js` et le pie chart généré avec `recharts`.

```javascript
import React from 'react';

import { useLoaderData } from 'react-router';
import CharacterDetail from '../components/CharacterDetail';
import D3PieChart from '../components/D3PieChart';
import RechartsPieChart from '../components/RechartsPieChart';

const CharacterDetailPage = () => {
    // retrieve the character using the useLoaderData hook
    const character = useLoaderData();

    document.title = `${character.name} | Marvel App`;

    return (
        <>
            <CharacterDetail character={character} />

            <h2>Capacities</h2>
            <div style={{ display: 'flex'}}>
                <div style={{flex: '50%'}}>
                    <h3>Using D3</h3>
                    <D3PieChart data={character.capacities} />
                </div>
                <div style={{flex: '50%'}}>
                    <h3>Using Recharts</h3>
                    <RechartsPieChart data={character.capacities} />
                </div>
            </div>
        </>
    );
};

export default CharacterDetailPage;
```