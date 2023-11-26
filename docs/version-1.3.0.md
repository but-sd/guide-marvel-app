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

Créer le module utilitaire `src/components/chart-utils.js` qui contiendra les fonctions utilitaires permettant de transformer les données pour les rendre compatibles avec `d3.js` et `recharts`.

```javascript
/**
 * Prepare the data for the pie chart
 * @param {*} data 
 * @returns 
 */
export const prepareData = (data = []) => {
    const transformData = [
        { name: 'Force', value: data?.force },
        { name: 'Intelligence', value: data?.intelligence },
        { name: 'Energy', value: data?.energy },
        { name: 'Speed', value: data?.speed },
        { name: 'Durability', value: data?.durability },
        { name: 'Fighting', value: data?.fighting }
    ];

    // Remove the elements with undefined values
    return transformData.filter((element) => { return element.value !== undefined; });
}
```

La fonction `prepareData` prend en paramètre les données à afficher. Elle retourne un tableau avec les données au format attendu par `d3.js` (un tableau d'objets avec les propriétés `name` et `value`) en supprimant les données avec une valeur `undefined`. 

Le fait d'externaliser cette fonction permettra de l'utiliser dans les deux implémentations du pie chart. Mais aussi de la tester unitairement.

Créer le test unitaire `src/components/chart-utils.test.js` pour tester la fonction `prepareData`.

```javascript
import { prepareData } from "./chart-utils";

describe('prepareData', () => {
    test('prepareData with empty data', () => {
        // given
        const data = {};

        // when
        const preparedData = prepareData(data);

        // then
        expect(preparedData).toEqual([]);
    });

    test('prepareData with data', () => {
        // given
        const data = {
            force: 10,
            intelligence: 20,
            energy: 30,
            speed: 40,
            durability: 50,
            fighting: 60,
        };

        // when
        const preparedData = prepareData(data);

        // then
        expect(preparedData).toEqual([
            { name: 'Force', value: 10 },
            { name: 'Intelligence', value: 20 },
            { name: 'Energy', value: 30 },
            { name: 'Speed', value: 40 },
            { name: 'Durability', value: 50 },
            { name: 'Fighting', value: 60 },
        ]);
    });

    test('prepareData with data with undefined values', () => {
        // given
        const data = {
            force: undefined,
            intelligence: 20,
            energy: 30,
            speed: 40,
            durability: undefined,
            fighting: 60,
        };

        // when
        const preparedData = prepareData(data);

        // then
        expect(preparedData).toEqual([
            { name: 'Intelligence', value: 20 },
            { name: 'Energy', value: 30 },
            { name: 'Speed', value: 40 },
            { name: 'Fighting', value: 60 },
        ]);
    });

    test('prepareData with data with null values', () => {
        // given

        // when
        const preparedData = prepareData();

        // then
        expect(preparedData).toEqual([]);
    });
});
```

Les tests unitaires permettent de vérifier que la fonction `prepareData` fonctionne correctement en fonction des données passées en paramètre.


***CharacterDetailPage***

Modifier le composant `src/pages/CharacterDetailPage.js` afin d'afficher le graphique D3.js et plus tard le graphique Recharts. 

```javascript
import React from 'react';

import { useLoaderData } from 'react-router';
import CharacterDetail from '../components/CharacterDetail';
import D3PieChart from '../components/D3PieChart';
// import RechartsPieChart from '../components/RechartsPieChart';

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
                    {/* <RechartsPieChart data={character.capacities} /> */}
                </div>
            </div>
        </>
    );
};

export default CharacterDetailPage;
```

### `d3.js`

`d3.js` est une librairie JavaScript qui permet de manipuler le DOM pour créer des visualisations de données. Elle est très utilisée dans le monde du web pour créer des graphiques, des cartes, des diagrammes, etc.

Installer `d3.js` avec `npm`:

```bash
npm install d3
```



Créer le composant `src/components/D3PieChart.js` et implémenter le graphique avec `d3.js`.

```javascript
import PropTypes from 'prop-types';
import { useEffect } from "react";
import * as d3 from "d3";
import { prepareData } from './chart-utils';

/**
 * Draw the pie chart
 * @param {*} data 
 * @param {*} displayTooltip 
 * @param {*} displayValue 
 */
const drawChart = (data) => {
    // Remove the old svg
    d3.select('#pie-container')
        .select('svg')
        .remove();

    // Create the color scale
    const color = d3.scaleOrdinal()
        // colors based on data
        .domain(data.map(d => d.name))
        // .range(["red", "blue", "green", "yellow", "orange", "purple"]);
        .range(d3.schemeDark2);
        //.range(d3.quantize(t => d3.interpolateSpectral(t * 0.8 + 0.1), filteredData.length).reverse());

    // Define the diameter of the pie
    const diameter = 100;

    // Define the margin
    const margin = {
        top: 10, right: 10, bottom: 10, left: 10,
    };

    // Define the width and height using the margin conventions
    const width = 2 * diameter + margin.left + margin.right;
    const height = 2 * diameter + margin.top + margin.bottom;

    // Define the radius
    const radius = Math.min(width, height) / 2;

    // Create the arc
    const arc = d3.arc()
        .cornerRadius(5) // Rounded corners
        .innerRadius(radius * 0.5) // This is the size of the donut hole
        .outerRadius(radius) // This is the size of the donut
        .padAngle(0.011) // padding between slices

    // Create the pie
    const pie = d3.pie(data)
        .sort(null) // disable sorting of data
        .value(d => d.value);

    // Create the svg, with the right dimensions
    const svg = d3
        .select('#pie-container')
        .append('svg')
        .attr("width", width)
        .attr("height", height)
        .attr("viewBox", [-width / 2, -height / 2, width, height]) // center the pie chart

    // draw the donut
    svg.append("g")
        .selectAll()
        .data(pie(data))
        .join("path")
        .attr("fill", d => color(d.data.name))
        .attr("d", arc)

    // add labels over the donut
    svg.append("g")
        // text style
        .attr("font-family", "sans-serif")
        .attr("font-size", 12)
        .attr("text-anchor", "middle")
        .selectAll()
        .data(pie(data))
        .join("text")
        // center the text
        .attr("transform", d => `translate(${arc.centroid(d)})`)
        // add the name of the data
        .call(text => text.append("tspan")
            .attr("id", d => `pie-labels-name-${d.data.name}`)
            .attr("x", 0) // center the text
            .attr("y", "-0.4em") // add a space between the name and the value
            .attr("font-weight", "bold")
            .text(d => d.data.name))
        // add the value of the data
        .call(text => text.filter(d => (d.endAngle - d.startAngle) > 0.25).append("tspan")
            .attr("id", d => `pie-labels-value-${d.data.name}`)
            .attr("x", 0) // center the text
            .attr("y", "0.7em") // add a space between the name and the value
            .attr("fill-opacity", 0.7) // make it lighter
            .text(d => d.data.value)); // add the value
};

/**
 * Draw a pie chart with the statistics of a character
 * 
 * @param {*} data
 * @param {*} displayTooltip
 * @param {*} displayValue
 */
export default function D3PieChart({
    data,
}) {
    // useEffect is a hook that will run the code inside it only once when data is loaded
    useEffect(() => {
        // transform data
        const preparedData = prepareData(data);

        // draw the chart
        drawChart(preparedData);
    }, [data]);

    return (
        // Return the div that will contain the chart
        <div id="pie-container" />
    );
}

D3PieChart.propTypes = {
    data: PropTypes.shape({
        force: PropTypes.number,
        intelligence: PropTypes.number,
        energy: PropTypes.number,
        speed: PropTypes.number,
        durability: PropTypes.number,
        fighting: PropTypes.number,
    }),
};

```

Le composant `D3PieChart` génère une div avec l'id `pie-container` qui sera utilisée pour afficher le graphique. Le hook `useEffect` permet de lancer le code de la fonction `drawChart` uniquement lorsque les données sont chargées.

La fonction `drawChart` permet de dessiner le graphique. Elle prend en paramètre les données à afficher. Elle utilise la librairie `d3.js` pour dessiner le graphique. Il n'y a pas de spécificité React dans cette fonction.

Tout d'abord, on supprime le graphique précédent, s'il existe.

On définit ensuite les informations nécessaires pour dessiner le graphique : la couleur, les dimensions du graphique (marges, largeur, hauteur, rayon...).

La couleur est définie à l'aide de la fonction `d3.scaleOrdinal()`. Cette fonction permet de définir une échelle de couleur. On lui passe en paramètre un tableau avec les couleurs à utiliser. On peut utiliser des couleurs prédéfinies avec `d3.schemeDark2` ou `d3.quantize(t => d3.interpolateSpectral(t * 0.8 + 0.1), filteredData.length).reverse()`.

On crée ensuite l'arc avec la fonction `d3.arc()`. Cette fonction permet de définir la forme des arcs du graphique. On définit la taille du trou au centre du graphique avec `innerRadius` (afin de créer un donut chart) et la taille du graphique avec `outerRadius`.

La fonction `d3.pie()` permet de définir le type de graphique à dessiner. On lui passe en paramètre les données à afficher. On peut définir le tri des données avec `sort` et la valeur à utiliser pour dessiner le graphique avec `value`.

On crée ensuite le svg avec la fonction `d3.select()`. On lui passe en paramètre l'élément du DOM dans lequel on veut dessiner le graphique. On définit ensuite les dimensions du svg afin qu'il prenne toute la place disponible. On centre le graphique avec `viewBox`.

On dessine ensuite le donut, puis on ajoute les labels. 

La documentation de `d3.js` est disponible à l'adresse [https://d3js.org/](https://d3js.org/).

**Test unitaire**

Ajouter le test unitaire pour le composant `D3PieChart` dans le fichier `src/components/D3PieChart.test.js`.

Pour tester le composant `D3PieChart`, on peut vérifier :

- que le svg est bien dessiné
- que les labels sont bien dessinés
- qu'il y a bien 6 arcs 

```javascript
import { render } from '@testing-library/react';
import D3PieChart from './D3PieChart';

describe('D3PieChart', () => {
    test('renders without error', () => {
        render(<D3PieChart data={{}} />);
    });

    test('renders the pie chart with correct data', () => {
        // when
        const data = {
            force: 10,
            intelligence: 20,
            energy: 30,
            speed: 40,
            durability: 50,
            fighting: 60,
        };

        // then
        render(<D3PieChart data={data} />);

        // expect to have a pie chart container
        expect(document.getElementById('pie-container')).toBeInTheDocument();

        // expect to have a svg element
        const svgElement = document.querySelector('svg');
        expect(svgElement).toBeInTheDocument();

        // expect to have a path element for each data
        const pathElements = document.querySelectorAll('path');
        expect(pathElements).toHaveLength(Object.keys(data).length);

        expect(svgElement.getElementById('pie-labels-name-Force')).toBeInTheDocument();
        expect(svgElement.getElementById('pie-labels-name-Intelligence')).toBeInTheDocument();
        expect(svgElement.getElementById('pie-labels-name-Energy')).toBeInTheDocument();
        expect(svgElement.getElementById('pie-labels-name-Speed')).toBeInTheDocument();
        expect(svgElement.getElementById('pie-labels-name-Durability')).toBeInTheDocument();
        expect(svgElement.getElementById('pie-labels-name-Fighting')).toBeInTheDocument();
    });
});
```

<!-- S'inspirer de [https://d3-graph-gallery.com/graph/donut_label.html](https://d3-graph-gallery.com/graph/donut_label.html){target="_blank"} pour générer un pie chart avec les capacités des personnages.

Le tutoriel [https://www.tutorialsteacher.com/d3js/create-pie-chart-using-d3js](https://www.tutorialsteacher.com/d3js/create-pie-chart-using-d3js){target="_blank"} explique comment créer un pie chart avec `d3.js`.

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

La documentation de `d3.js` est disponible à l'adresse [https://d3js.org/](https://d3js.org/). -->

<!-- Committer et pusher les modifications.

Ajouter le test unitaire pour le composant `D3PieChart` dans le fichier `src/components/D3PieChart.test.js`, github copilot peut vous aider à écrire le test (bouton droit sur le composant `D3PieChart` puis `Copilot / Generate tests`). 

Attention à bien vérifier le test généré par github copilot et à le modifier afin d'ajouter les vérifications nécessaires. Par exemple pour ce type de composant, on peut vérifier :

- que le svg est bien dessiné
- que les labels sont bien dessinés
- qu'il y a bien 6 arcs -->

### recharts

`Recharts` est une librairie React qui permet de créer des graphiques. Elle est basée sur `d3.js`. Elle permet de créer des graphiques manipulant des composants React. Cela peut être plus simple à utiliser que `d3.js` pour des développeurs React, mais elle est moins flexible que `d3.js`. 

Installer `recharts` avec `npm`:

```bash
npm install recharts
```

Décommenter le composant `RechartsPieChart` dans le fichier `src/pages/CharacterDetailPage.js`.

Créér le composant `src/components/RechartsPieChart.js` et implémenter le graphique avec `recharts`.

```javascript
import PropTypes from 'prop-types';
import { PieChart, Pie, Tooltip, Cell } from 'recharts';
import { prepareData } from './chart-utils';

const RechartsPieChart = ({ data }) => {
    // Prepare the data
    let transformedData = prepareData(data);

    // Define the colors
    const COLORS = ['#0088FE', '#00C49F', '#FFBB28', '#FF8042', '#8884d8', '#82ca9d'];

    return (
        <PieChart width={300} height={224} >
            <Pie dataKey="value" cx={100} cy={100} data={transformedData} innerRadius={40} outerRadius={80} label>
                {
                    transformedData.map((entry) => <Cell key={`cell-${entry.name}`} fill={COLORS[transformedData.indexOf(entry) % COLORS.length]} />)
                }
            </Pie>
            <Tooltip />
        </PieChart>
    );
}

RechartsPieChart.propTypes = {
    data: PropTypes.shape({
        force: PropTypes.number,
        intelligence: PropTypes.number,
        energy: PropTypes.number,
        speed: PropTypes.number,
        durability: PropTypes.number,
        fighting: PropTypes.number,
    }),
};

export default RechartsPieChart;
```

Le composant `RechartsPieChart` génère un graphique avec la librairie `recharts`. Il prend en paramètre les données à afficher. Il transforme les données pour les mettre dans le format attendu par `recharts`. Il utilise ensuite les composants `PieChart`, `Pie`, `Tooltip` et `ResponsiveContainer` de `recharts` pour dessiner le graphique.

Voir la documentation de `recharts` à l'adresse [https://recharts.org/en-US/](https://recharts.org/en-US/){target="_blank"}. Et plus particulièrement la documentation sur les pie charts à l'adresse [https://recharts.org/en-US/examples/PieChartWithPaddingAngle](https://recharts.org/en-US/examples/PieChartWithPaddingAngle){target="_blank"}.

**Test unitaire**

Ajouter le test unitaire pour le composant `RechartsPieChart` dans le fichier `src/components/RechartsPieChart.test.js`.

Pour tester le composant `RechartsPieChart`, celui-ci étant basé sur `recharts`, on ne peut pas tester le graphique directement. On peut tester que les données sont bien transformées avec la fonction `prepareData` et que le composant est bien rendu.

```javascript
import { render } from '@testing-library/react';
import RechartsPieChart from './RechartsPieChart';

describe('RechartsPieChart', () => {
    test('renders the pie chart with correct data', () => {
        // when
        const data = {
            force: 80,
            intelligence: 90,
            energy: 70,
            speed: 85,
            durability: 75,
            fighting: 95
        };

        // then
        render(<RechartsPieChart data={data} />);

        // expect to be ok
        expect(true).toBe(true);

        // expect to have a div with the class "recharts-wrapper"
        expect(document.querySelector('.recharts-wrapper')).toBeInTheDocument();
    });

    test(' don\'t fail when data is null', () => {
        // when
        const data = null;

        // then
        render(<RechartsPieChart data={data} />);

        // expect to have a div with the class "recharts-wrapper"
        expect(document.querySelector('.recharts-wrapper')).toBeInTheDocument();
    });
});
```

Du fait que le composant `RechartsPieChart` est basé sur `recharts`, on ne doit pas tester le graphique directement. En effet, `recharts` est une librairie externe, on ne doit pas tester son code, on n'en a pas la responsabilité et le code pourrait changer à tout moment.

On peut par contre tester que le composant est bien rendu.

**Adapter les tests unitaires**

Modifier le fichier `src/pages/CharacterDetailPage.test.js` afin de prendre en compte les modifications apportées au composant `CharacterDetailPage`.

```javascript
import { render, screen } from '@testing-library/react';
import CharacterDetailPage from './CharacterDetailPage';
import { BrowserRouter } from 'react-router-dom';

// fix for ResizeObserver not being defined in Jest
const { ResizeObserver } = window;

beforeEach(() => {
    delete window.ResizeObserver;
    window.ResizeObserver = jest.fn().mockImplementation(() => ({
        observe: jest.fn(),
        unobserve: jest.fn(),
        disconnect: jest.fn()
    }));
});

afterEach(() => {
    window.ResizeObserver = ResizeObserver;
    jest.restoreAllMocks();
});

// end fix for ResizeObserver not being defined in Jest

const character = {
    id: "1",
    name: "Thor",
    description: "Thor description",
}

// mock the useLoaderData hook, so that we can test the CharacterDetailPage component
jest.mock('react-router', () => ({
    ...jest.requireActual('react-router'), // use actual for all non-hook parts
    useLoaderData: () => {
        return character;
    },
}));

describe('CharacterDetailPage', () => {

    test('render CharacterDetailPage component', () => {
        // when

        // then
        render(<CharacterDetailPage />, { wrapper: BrowserRouter });

        // expect the document title to be "Thor | Marvel App"
        expect(document.title).toBe(`${character.name} | Marvel App`);

        // expect to have a heading with the character name
        const h2Element = screen.getByRole('heading', { level: 2, name: character.name });
        expect(h2Element).toBeInTheDocument();

        // expect to have a paragraph with the character description
        const pElement = screen.getByText(character.description);
        expect(pElement).toBeInTheDocument();

        // expect to have a heading with the text "Capacities"
        const h2CapacitiesElement = screen.getByRole('heading', { level: 2, name: 'Capacities' });
        expect(h2CapacitiesElement).toBeInTheDocument();

        // expect to have a heading with the text "Using D3"
        const h3D3Element = screen.getByRole('heading', { level: 3, name: 'Using D3' });
        expect(h3D3Element).toBeInTheDocument();

        // expect to have a heading with the text "Using Recharts"
        const h3RechartsElement = screen.getByRole('heading', { level: 3, name: 'Using Recharts' });
        expect(h3RechartsElement).toBeInTheDocument();

        // expect to have a div with the id "pie-container"
        expect(document.getElementById('pie-container')).toBeInTheDocument();

        // expect to a an div with class "recharts-wrapper"
        expect(document.querySelector('.recharts-wrapper')).toBeInTheDocument();
    });
});
```

Ici on ajoute juste la vérification que les éléments du graphique sont bien présents dans le DOM, on ne vérifie pas qu'ils sont bien dessinés (cette vérification est faite dans les tests unitaires des composants `D3PieChart` et `RechartsPieChart`).

`recharts` utilise `ResizeObserver` pour redessiner le graphique lorsque la taille de la fenêtre change. Il faut donc ajouter un mock pour `ResizeObserver` afin de ne pas avoir d'erreur lors de l'exécution des tests unitaires.

### Comparaison des deux librairies

L'avantage de `d3.js` est qu'elle est très flexible du fait qu'elle manipule directement le DOM. On peut donc faire des graphiques très personnalisés. Par contre, il faut avoir des connaissances en `d3.js` pour pouvoir l'utiliser. Elle n'est pas liée à React, il faut donc faire attention à bien intégrer le graphique dans le cycle de vie de React, mais à contrario, on peut l'utiliser dans d'autres frameworks ou même sans framework (avec du JavaScript pur).

`recharts` est plus simple à utiliser que `d3.js` et permet de créer des graphiques rapidement, toute la complexité est cachée dans les composants React. Par contre, elle est moins flexible que `d3.js` et il peut être difficile de faire des graphiques très personnalisés. Elle est liée à React, il n'est donc pas possible de l'utiliser dans d'autres frameworks ou avec du JavaScript pur.

## Librairie externe

Lors de l'utilisation d'une librairie externe, il faut bien vérifier la documentation et les exemples fournis afin de bien comprendre comment l'utiliser. Est-ce que la librairie est bien adaptée à notre besoin ? Est-ce que la librairie est facile à utiliser ? Est-ce que la librairie est bien maintenue ? Est-ce que la librairie est utilisée par la communauté ? Est-ce que je peux utiliser la librairie dans mon projet ? Est-ce que la librairie est payante ?

### Maintenance / Communauté

En effet, si la librairie n'est plus maintenue, elle peut devenir obsolète et ne plus fonctionner avec les nouvelles versions des navigateurs et rendre notre application obsolète. C'est un risque à prendre en compte lors de l'utilisation d'une librairie externe.

Si la librairie est utilisée par la communauté, cela signifie qu'elle est utilisée par d'autres développeurs et qu'il y a donc plus de chance qu'elle soit maintenue, que les bugs soient corrigés et que de nouvelles fonctionnalités soient ajoutées. 

Il est plus facile de trouver de l'aide sur internet, de même que des exemples d'utilisation. Des outils d'IA comme github copilot s'appuient sur les exemples d'utilisation de la librairie pour générer du code.

### Licence

Il est nécessaire de vérifier la licence de la librairie afin de savoir si l'on peut l'utiliser dans notre projet. Certaines librairies peuvent être payantes ou avoir des licences restrictives.

Par exemple une licence MIT permet d'utiliser la librairie dans un projet commercial, alors qu'une licence GPL impose que le projet soit open source. 

Pour des projets hébergés sur github l'information sur la licence est disponible dans le fichier `LICENSE` à la racine du projet. github affiche ainsi quelques informations sur le type de licence et les conditions d'utilisation liées à la licence.

Par exemple la licence de `d3.js` est une licence ISC, qui est une licence MIT modifiée. Elle permet d'utiliser la librairie dans un projet commercial. [https://github.com/d3/d3/blob/main/LICENSE](https://github.com/d3/d3/blob/main/LICENSE){target="_blank"}

La licence de `recharts` est une licence MIT. [https://github.com/recharts/recharts/blob/master/LICENSE](https://github.com/recharts/recharts/blob/master/LICENSE){target="_blank"}


### Documentation

Il faut aussi vérifier la documentation de la librairie afin de bien comprendre comment l'utiliser. 

Est-ce que la documentation est à jour ? complète ? facile à comprendre ? contient des exemples d'utilisation ? ...

### Sécurité

Est-ce qu'elle ne contient pas de failles de sécurité ? Est-ce que les failles de sécurité sont corrigées rapidement ?

Des outils existent pour vérifier si une librairie contient des failles de sécurité.

**npm audit**

`npm audit` va vérifier les librairies utilisées par notre projet et va afficher les failles de sécurité trouvées. 


```bash
npm audit
```

Extraits de la sortie de la commande `npm audit` pour le projet `marvel-app`:

```bash
Axios  0.8.1 - 1.5.1
Severity: moderate
Axios Cross-Site Request Forgery Vulnerability - https://github.com/advisories/GHSA-wf5p-g6vw-rhxx
fix available via `npm audit fix --force`
Will install browser-sync@2.23.7, which is a breaking change
node_modules/axios
  localtunnel  >=1.9.0
  Depends on vulnerable versions of axios
  node_modules/localtunnel
    browser-sync  >=2.24.0-rc1
    Depends on vulnerable versions of localtunnel
    ...
```

npm audit va afficher les failles de sécurité trouvées, leur niveau de criticité et les librairies concernées. 

Il est possible de corriger automatiquement (en fonction du numéro de version de la librairie, semver) certaines des failles de sécurité avec la commande `npm audit fix`, si la montée de version n'implique pas de breaking change. 

```bash
npm audit fix
```

Attention, même si la montée de version n'implique pas de breaking change, il est possible que la mise à jour de la librairie casse notre application. La présence de tests unitaires avec une couverture de code suffisante permet de vérifier que la mise à jour ne casse pas notre application.

On peut aussi utiliser l'option `--force` pour forcer la mise à jour des librairies.

```bash
npm audit fix --force
```

Attention l'option `--force` veut dire qu'on ne tient pas compte des éventuels problèmes de compatibilité avec les nouvelles versions des librairies. Il y a donc un risque que la mise à jour des librairies casse notre application. 

Cette commande est à utiliser avec précaution et plutôt lorsque l'on souhaite mettre à jour les librairies de notre projet et que l'on est prêt à corriger les éventuels problèmes de compatibilité. 

**Tests unitaires**

Lors de la rédaction des tests unitaires, il faut faire attention à ne pas tester le code de la librairie externe. On n'en a pas la responsabilité et le code pourrait changer à tout moment. On doit donc tester uniquement notre code, c'est à dire les données que l'on passe à la librairie externe et le fait que le composant soit bien rendu.

## Release 1.3.0

Committer et pusher les modifications et effectuer la release `1.3.0`.



