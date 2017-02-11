# Variables

## Portée de block : `const` et `let`

### block
Portée de block `{}` plutôt que portée lexicale.

```js
// Blocks
if( true ){ let it = "be";  }

// let keep i in the loop scope
const courses = [ "JS", "HTML", "CSS" ];
for( let i=0, l=courses.length; i<l; i++ )
{
	console.log( courses[ i ] );
}
```

> **Note** `let` est déclaré (_hoisting_ au début du block),tandis que les déclarations `var` le sont au début de la `function`.

### portée de la variable plus précise que la portée de la fonction

```js
// en es5
for (var i = 1; i < 6; i++)
{
	Meteor.setTimeout
	(
		function ()
		{
			console.log(i);
		}, 0
	); //=> 6 6 6 6 6 -- probably not our intention!
}

```

```js
// en es2015
for (let i = 1; i < 6; i++)
{
	Meteor.setTimeout
	(
		function ()
		{
			console.log(i);
		}, 0
	); //=> 1 2 3 4 5 -- kept i's value for each iteration
}
console.log(i); //=> error/undefined -- safe
```

## Subtilités de `const`

Attention, les valeurs constantes ne fonctionnent que sur les valeurs primitives, pas les référénces.
Les constantes ne sont donc pas _immutable_.

```js
const cantchange = 0;	
// TypeError: Assignment to constant variable.
// cantchange = 1;


// Beware const don't forbid object's values change
const prof = { name : "eric" };
prof.name = "Eric";
```

> **Warning** Affecter une `const` après son initialisation echoue silencieusement (ou bruillament – par une exception – en `strict mode`)

## Temporal Dead Zone

> **TODO** See [ES6 Let, Const and the “Temporal Dead Zone” (TDZ) in Depth](https://ponyfoo.com/articles/es6-let-const-and-temporal-dead-zone-in-depth)


## Références

- [Introduction to ES2015](https://tutor.mantrajs.com/say-hello-to-ES2015/let-const)
- 