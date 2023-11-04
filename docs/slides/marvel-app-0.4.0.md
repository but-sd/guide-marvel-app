---
marp: true
theme: gaia
size: 16:9
paginate: true
backgroundImage: url('https://marp.app/assets/hero-background.jpg')
header: 'marvel-app - 0.4.0'
footer: 'Auteur : Alexandre GIRARD'
---

# Marvel App - 0.4.0

## Objectifs

- Création de pages
- Navigation entre les pages
    - layout
    - routes
    - links

---

## Création de pages

Une page est un composant React comme les autres. Elle peut être composée d'autres composants React.

- Création des pages
    - About: page d'information sur l'application
    - Contact: page de contact
    - Home: page d'accueil

---

## Navigation entre les pages

### Layout

Le layout est un composant React qui va être affiché sur plusieurs pages de l'application.

Le layout contient les éléments communs à toutes les pages de l'application.

---

## Navigation entre les pages

### Routes

Les routes permettent de définir quel composant React doit être affiché en fonction de l'URL.

---

## Navigation entre les pages

### Links

Les links permettent de créer des liens entre les pages de l'application.

react-router propose 2 types de links :

- Link: permet de créer un lien vers une page de l'application
- NavLink: permet de créer un lien vers une page de l'application et de le mettre en surbrillance
