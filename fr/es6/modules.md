# Modularité du code

Les modules permettent de répartir votre code dans plusieurs fichiers dont certaines dépendances seront partagées.

## Exemple
Un petit exemple réparti sur plusieurs fichiers.

### `exports`

```js
// lib/math.js
export function sum( x, y )
{
	return x + y;
}
export var pi = 3.141593;
```

### named `import`
```js
// app.js
import * as math from "lib/math";
console.log( "2π = " + math.sum( math.pi, math.pi ) );
```

### multiple `import`
```js
// otherApp.js
import {sum, pi} from "lib/math";
console.log( "2π = " + sum( pi, pi ) );
```

### `default` export

```js
// Default export value
export default function( x )
{
	return Math.exp( x );
}
```

```js
import exp from "lib/math";

```

## A savoir

- Tous les modules utilisent par défaut le mode strict. Aucun besoin de déclarer `"use strict"` dedans.
- **L'inclusion des modules est synchrone**.

## Références

- [ES6 In Depth: Modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)