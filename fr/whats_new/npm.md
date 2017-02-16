# Intégration avec NPM

Auparavant, le gestionnaire de package recommandé était [Atmosphere](https://atmospherejs.com/). Celui-ci avait comme spécificité d'héberger des dépendances prévues pour _l'isomorphisme_, façon `meteor.js`. 

Toutefois, le [registre NPM](https://www.npmjs.com/), très populaire au sein de la communauté, propose de nombreuses solutions, prête à l'emploi.

Bien que la reprise de librairies provenant de ce registre était possible par le passé, elle devient aujourd'hui, le principe oficiel retenu. A terme, il est d'ailleurs prévu que l'ensemble de la lirairies `meteor.js` migre vers cette plateforme.

Et vu la très grande diversité des sources disponibles, il est viviement recommandé  de s'y référer souvent, sous peine de "réinventer la roue" !

## Mémo package Atmosphere

Rappelons-nous, pour ajouter un package, nous utilisions la syntaxe :

```sh
meteor add nom_du_package
```

Après une installation réussie, les dépendances de ce dernier se trouvaient disponibles à l'utilisation. En effet, elles résidaient dans un répertoire invisible, nommé `.meteor`, situé à la racine du projet.

Dans ce répertoire, un fichier texte `packages` liste toutes les dépendances utilisées. D'ailleurs, vous pouvez intervenir directement dessus, et supprimer les dépendances inutiles ; le compilateur `meteor`les supprimera automatiquement.

## Package `npm`

Pour sa part, un package `npm` est représenté par un fichier `package.json` 

```json
{
	"name": "eat-sandwich",
	"version": "1.0.0",
	"description": "You call yourself a sandwich eater?",
	"author": "Doug Funnie <doug.funnie@bluffington.edu>",
	"license": "MIT"
}
```

et un fichier

```js
exports.eatSandwich = () =>
{
	console.log('Oh yeah, now we\'re eating sandwiches!'); 
}
```

### Installation

Les sources de la librairie [moment.js](https://www.npmjs.com/package/moment) seront disponibles pour notre projet ainsi :

```sh
npm i moment --save
```

- le paramètre `i` est un raccourci pour `install`.
- `--save` permet de tenir à jour le fichier de description `package.json` de notre propre projet.

> **Warning** Il est absolument nécessaire d'utiliser le paramètre `--save`. En effet, son omission ne permettra à d'autres utilisateurs de télécharger les dépendances nécessaires au projet, **notamment dans le cas d'un projet développé à plusieurs, ou via un système de versioning.**

<p/>

> **Note** npm permet également d'installer des libraires de façon globale, c'est-à-dire disponibles à tout le système d'exploitation.
```sh
npm i grunt-cli --global
```

### `node_modules`

Dans ce répertoire toutes les dépendances npm seront organisées.

> **Hint** Pensez à l'exclure de votre système de versioning, via `.gitignore` par exemple. Autrement, toutes les ressources liées seraient incluses, alourdisssant par la même votre _repository_.

### Workflow `npm`

Lorsqu'une personne clone votre projet, il lui faudra au préalable télécharger les librairies liées afin de le faire fonctionner.

```sh
meteor npm i
```

Cette commande va lancer un processus de téléchargement de toutes les dépendances insérée dans le fichier `package.json`. Elles se trouveront au fur et à mesure dans le répertoire `node_module`.

### `meteor npm` 

Si vous n'avez pas installer la librairie `npm` accessible globalement sur votre poste de travail, `meteor` fournit un version locale

```sh
 meteor npm <command>
```

Toutes les commandes `npm` sont ainsi disponibles à tout projet.

## Utilisation des packages

Toutes les dépendances installées via `npm` sont disponibles avec des références locales :

```js
import moment from 'moment';
```
inclut une référence à la librarie `moment` dans votre code.

> **Note** L'import des librairies npm peut omettre l'extension du fichier, par contre, par convention, [il est préférable d'inclure le nom de l'extension pour vos fichiers](../best_practices/conventions.md).

### Feuilles de style

`meteor` supporte les _transpilers_ suivant :

- [less](http://lesscss.org/) via le package atmosphere meteor `less`
- [sass](http://sass-lang.com/) via le package atmosphere `fourseven:scss`
- [stylus](http://stylus-lang.com/) via le package atmosphere meteor `stylus`

Vous incluerez le résulat dans le `<head><style></style></head>` grâce à un import.

- Chemin global
```js
@import '{}/node_modules/npm-package-name/button.less';
```
- Chemin relatif
```js
@import '../../node_modules/npm-package-name/colors.less';
``` 

### Legacy meteor modules

> **Note** Les `import` utilisent des chemins relatifs, et inclus le nom de l'extension du fichier (contraierement à node.js).
Les packages _Atmosphere_ et les API de meteor, utilisent des `export` contenant plusieurs dépendances. Elles sont accsessibles de cette façon 

```js
// You'll need to destructure here, as Meteor could export more symbolsimport { Meteor } from 'meteor/meteor';// This will not workimport Meteor from 'meteor/meteor';
``` 

## Références

- [Using NPM Packages](https://themeteorchef.com/tutorials/using-npm-packages?utm_source=The+Meteor+Chef+-+Weekly+Digest&utm_campaign=b2e307f3f5-Weekly_Digest_January_13th_2017&utm_medium=email&utm_term=0_a347eecb12-b2e307f3f5-412955113)