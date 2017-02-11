# function


## `function` expression et `function` declaration

Petit rappel sur les deux syntaxes pour les fonctions.

### Function declaration

Une _function declaration_ définit une fonction nomnée **sans** l'affectation d'une variable. Il s'agit d'une stucture autonome qui ne peut être incluse autre part que dans un block de `function`, tel q'une variable, une propriété d'objet ou une valeur de tableau.
Il est intéressant de voir cette syntaxe telle la sœur d'une déclaration de variable. La déclaration des varaibales débutent avec `var`, les _function declaration_ avec `function`.

Ainsi déclarée, son nom est accessibledans sa portée parente.

### Function expression

Une `function expression` definit une `function` comme une partie plus large d'une expression (typiquement une affectation de variable).
Elles peuvent soit nommées, soit anonymes.
Elles n'ont pas besoin de débuter par le mot clé `function` (d'où les paranthèses autour des _self invoking functions_)

## Paramètres par défaut

```js
let ditesUnNombre = ( combien = 33 ) => combien;  
```

> **Note** Les valeurs par défaut sont des expressions, elles sont calculées avant d'être employées !

## Nouvelle syntaxe, arrow function

Vu l'usage très fréquent des fonctions, une syntaxe raccourcie a vue le jour.

### Cas d'un paramètre unique
```js
// ES5 lambdas-like
var numbers = [ 10, 20, 30, 50 ];
var multiplyBy10 = numbers.map
 (
     function( a )
     {
         return a * 10;
     }
 );
console.log( multiplyBy10 );

// ...becomes in ES2015
const numbers      = [ 10, 20, 30, 50 ];
const multiplyBy10 = numbers.map( a => a * 10 );
console.log( multiplyBy10 );
```

Lorsqu'un seul paramètre est nécessaire, la syntaxe `Identifier => Expression` suffit.

> **Note** Le `return` est implicite en fin de _statement_.

### Cas de plusieurs paramètres

On utilise des parenthèses dans les cas où, il y a :
- plusieurs paramètres 
- aucun paramètre
- paramètre _rest_ 
- un ou des paramètres par défaut
- des paramètres déconstruits (_deconstructuring parameters_)

```js
// With multiple arguments, add parenthesis
const numbers         = [ 10, 20, 30, 50 ];
const multiplyByIndex = numbers.map( ( a, i ) => a * i );
console.log( multiplyByIndex );
```

### Cas d'une structure objet à renvoyer

```js
// Beware if you need to return a structure, wrap it in parenthesis
const numbers      = [ 10, 20, 30, 50 ];
const multiplyBy10 = numbers.map( a => ({ res: a * 10 }) );
// not const multiplyBy10 = numbers.map( a => { res: a * 10 } );
console.log( multiplyBy10 );
```

### A savoir

- Les _arrow function_ ne disposent pas de déclaration nommée, seulement des expressions

```js
let it = () => "be";
``` 
- Pas de saut de ligne possible entre les paramètres et le coprs de la _function_
- Mieux indiquées pour déclarer les méthodes d'object

```js
var obj =
{
	i: 10,
	b: () => console.log(this.i, this)
}
```
- Attention, les _arrow function_ ne possèdent pas de _prototype_

## Portée des _arrow function_

**_Arrow functions_ ne dispose pas des mêmes règles de détermination de `this`.** Cette valeur automatique est toujours obtenue depuis la **portée lexicale parente**.

```js
// ES5 this
function Clock()
{
	this.currentTime = new Date();
};

Clock.prototype.start = function()
{
	var self = this;// Save scope in closure
	setInterval
	(
		function()
		{
			self.currentTime = new Date();
		}, 1000
	);
};

// ES6 with arrow functions,
// automatically scope this to its outer scope
// !! Beware !!
// Arrow function uses lexcial scope
Clock.prototype.start = function()
{
	setInterval
	(
		() =>
		{
			this.currentTime = new Date();
		}, 1000
	);
};
```

## References

- [Function Declarations vs. Function Expressions](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
- [ES6 In Depth: Arrow functions](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)
- [Mozilla Developper Network](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/Fonctions_fl%C3%A9ch%C3%A9es)