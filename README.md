# Game Of Life

Me tester avec l'exercice du [Jeux de la Vie](https://fr.wikipedia.org/wiki/Jeu_de_la_vie) avec [Nuxt 3](https://nuxtjs.org/) et [Tailwind](https://tailwindcss.com/docs/installation).

## Setup

Make sure to install the dependencies:

```bash
# npm
npm install

# yarn
yarn install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# yarn
yarn dev
```

## Done
- [x] Afficher une grille de 10x10
- [x] Afficher une cellule vivante (front)
- [x] Afficher une cellule morte (front)
- [x] Engine pour le system de "tick"
- [x] Démarer le system depuis un bouton
- [x] Stoper le system depuis un bouton
- [x] Récupérer les voisins d'une cellule

## Problème
Je pense me heurter à un problème de conception. 
J'aurais dû traiter les données métier avant de rendre mon front, car je me repose trop dessus. 
Mes class CSS ne devraient pas me donner l'information de l'état de la cellule. 
Je vais garder ce projet de côté pour m'en faire un exercice de refacto.

## Todo
- [ ] Refacto pour boolean au lieu de class CSS pour l'état de la cellule
- [ ] Refacto la fonction de récupération des voisins (getNeighborsResearched)
- [ ] Appliquer les règle métier de la vie sur les cellules.
- [ ] Maj de la grille en fonction de leurs états
- [ ] \+ Ajouter des tests (pas le but de l'exercice, mais c'est toujours bien de pratiquer)
- [ ] ++ Quelques animation pour rendre le tout plus sympa 