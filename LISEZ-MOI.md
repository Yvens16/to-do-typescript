## Concept

Ce template est conçu pour servir de base à tous les projets (P2/P3) suivants la stack React-Node-MySQL telle qu'enseignée à la Wild Code School. Il est préconfiguré avec un ensemble d'outils qui aideront les élèves à produire un code correspondant mieux aux standards du monde du travail et plus facile à maintenir, tout en restant simple à utiliser.

## Installation & Utilisation

### Pour commencer un projet

- Sur VSCode, installer les plugins **Prettier - Code formatter** et **ESLint** et les configurer
- Cloner ce dépôt, se rendre à l'intérieur
- Lancer la commande `npm run setup`
- _NB: Pour exécuter le backend, un fichier d'environnement avec les données de connexion d'une BdD valide est nécesaire. Un modèle se trouve dans `backend/.env.sample`_

### Liste des commandes et signification

- `setup` : Initialisation du frontend et du backend ainsi que des outils
- `dev` : Démarrage des deux serveurs (frontend + backend) dans un même terminal
- `dev-front` : Démarrage d'un serveur React pour le frontend
- `dev-back` : Démarrage d'un serveur Express pour le backend
- `lint` : Exécute des outils de validation de code (sera exécutée automatiquement à chaque _commit_)
- `fix` : Fixe les erreurs de formatage (à lancer si `lint` ne passe pas)

## Pour plus d'informations

### Listing des outils utilisés

- _Concurrently_ : Permet d'exécuter plusieurs commandes dans un même terminal
- _Husky_ : Permet d'exécuter des actions en déclenchement de commandes _git_
- _Vite_ : Alternative à _Create-React-App_, embarquant moins de packages pour une expérience plus fluide
- _ESLint_ : Outil de "qualité de code", permet de s'assurer que des règles pré-configurées sont bien respectées
- _Prettier_ : Outil de "qualité de code" également, se concentre plus particulièrement sur le style du code
- _Standard Airbnb_ : L'un des "standards" les plus connus, même s'il n'est pas officiellement lié à ES/JS
- _Nodemon_ : Outil permettant de relancer un serveur à chaque fois qu'un des fichiers est modifié

### Reste à faire

Prettier:

- corriger la config front/back pour qu'elle suive le même standard qu'ESLint

Testing:

- ajouter des tests unitaires sur le front et le back, avec les commandes associées

Vérifications:

- s'assurer que les principaux outils utilisés lors de la formation sont compatibles avec ce template
- deploiements ? Compatible avec Netlify/Vercel/Heroku ?
- fonctionnement avec yarn/pnpm

# Migration to TS

## Typescript part

1. cd frontend
2. npm i --save-dev typescript
3. tsc --init
4. Add in tsconfig.json
  1. "baseUrl": ".",
    "paths": {
      "@assets/*": ["src/assets/*"],
      "@components/*": ["src/components/*"],
      "@pages/*": ["src/pages/*"],
      "@services/*": ["src/services/*"]
    }
5. npm i @types/react --save-dev
6. uncomment " "jsx": "preserve", " line in tsconfig.json
7. In tsconfig.json: Under the object compilerOptions, add:
"include": [
    "src/**/*.ts",
    "src/**/*.d.ts",
    "src/**/*.tsx",
    "src/**/*.jsx",
    "src/**/*.vue",
    "tests/**/*.ts",
    "tests/**/*.tsx",
    "./*.d.ts"
    ],
8. Create a reacDom.d.ts for reactdom types and add in the file : declare module 'react-dom/client';
9. Under in frontend folder: create a svg.d.ts declaration file so ts undertant svg file
  1. Add this in the file:
  declare module "*.svg" {
  import React = require("react");
  export const ReactComponent: React.FC<React.SVGProps<SVGSVGElement>>;
  const src: string;
  export default src;
}
10. Change all .jsx files to .tsx files
11. dans index.html: change main.jsx to main.tsx


## ESlint typescript part

1. Change all .jsx references to tsx in the scripts: lint and fix in package.json
2. In eslintrc.json: Add the line under, in the rules object so Eslint is happy about jsx in tsx files: 
  1. "react/jsx-filename-extension": [2, { "extensions": [".js", ".jsx", ".ts", ".tsx"] }],
3. In eslinttrc.json: In the object "eslint-import-resolver-custom-alias" there is an extensions array
with ".js", ".jsx". 
  1. Add ".ts", ".tsx"
4. In the rules object: 
  1. Add "import/extensions": [
      "error",
      "ignorePackages",
      {
        "js": "never",
        "jsx": "never",
        "ts": "never",
        "tsx": "never"
      }
    ],

