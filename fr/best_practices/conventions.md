# Conventions

## Nommage

### Collections 

Les **collections** devraient adopter un nom au puriel, avec la notation _PascalCase_.
Le nom de la collection dans la base de données (1er argument dans le constructeur) devrait être identique.

```js
// Defining a collectionLists = new Mongo.Collection('Lists');
```

Les champs devraient adopter les mêmes normes que les variabales : débuter par une minuscule, soit en _CamelCase_.

### Méthodes et publications

Le nom des méthodes et publications names devraient adopter _CamelCase_, et utiliser un espace de nom, correspondant au module dans lequel elles résident :

- Méthode
```js
// in imports/api/todos/methods.jsMeteor.method
({	name: 'todos.updateText',  // ...});
```

- Publication :
```js
// Naming a publicationMeteor.publish
(
	'lists.public', function listsPublic()
	{	// ...	}
);
```

## Organisation du code

Le code devrait être organisé uniquement en modules, chargé depuis des clauses d'`import`.
Voir [l'intégration de NPM](../best_practices/structuration.md) pour une description sur le découpage des applications en modules.

Les fichiers devraient porter le même nom (en capitale si besoin) que le composant ou la classe qu'ils incluent.

```js
export default class ClickCounter { ... }
```

```js
import ClickCounter from './ClickCounter.js';
```
