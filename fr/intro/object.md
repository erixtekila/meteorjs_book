# Syntaxe des `Object` et `Array`

## Contruction
```js
// Object structure
const user =
{
  // No function anymore
  getName()
  {
      return 'Wowza !';
  }
};

console.log( user.getName() );
```

## Accesseurs

```js
function getCar(make, model, value)
{
    return {
        make,
        model,
 
        _value: value,
 
        get value() {
            return this._value;
        },
        set value(value) {
            if (value < 0)
                throw new Error('invalid value');
 
            this._value = value;
        }
    };
}
 
let car = getCar('Kia', 'Sorento', 40000);
 
// output: 40000
console.log(car.value);
 
car.value = 30000;
 
// error thrown
car.value = -1;
```

## Désconstruction

L'affectation par déconstruction permet d'assigner les propriétés d'un objet ou d'un tableau à des variables basées sur le même nom.

```js
// ES5
var first = someArray[0];
var second = someArray[1];
var third = someArray[2];

//ES2015
var [first, second, third] = someArray;
```

Cela fonctionne avec les object
```js
// Object construction
const name = 'Arunoda';
const age  = 80;

const user = { name, age };

// Object destructuration
const user =
{
  name: 'Eric',
  age : 20,
  city: 'Montreuil'
};

const { name, age } = user;
console.log( name, age );
```

Avec les fonctions, cette syntaxe est élégante:

```js
// Destructuring in functions
function printName( { name } )
{
	console.log( 'Name is: ' + name );
}

const user = 
{
	name: 'Eric',
	age : 20,
	city: 'Montreuil'
};

printName( user );

// or better
function printUser( { name, age = 20 /* default value */ } )
{
	console.log( 'Name is: ' + name + ' Age: ' + age );
}


// Destructuring works also with arrays
function printUser( [ name, age = 20 ] )
{
	console.log( 'Name is: ' + name + ' Age: ' + age );
}
```
 
## Spread

L'opérateur `...` (_rest_) est utilisé dans le cas des fonctions dites _variadic_. Ce sont des opérations qui peuvent recevoir un nombre changeant de paramètres.

```js
function sum( a, b )
{
	return a + b;
}

// rest parameter is spreading
function sumAndLog( ...args )
{
	const result = sum( ...args );
	console.log( 'Result is: ' + result );
	return result;
}

sumAndLog( 10, 20 );
```


## Cloner et fusionner

Le _rest_ opérateur devient pratique pour récupérer des valeurs d'une structure à l'autre.

```js
const user           = { name: "Eric" };
const newUser        = { ...user };
const withAge        = { ...user, age: 20 };
const newUserVersion = { age: 80, ...user };

console.log( newUser, withAge, newUserVersion );
```

Cette syntaxe marche également pour les tableaux

```js
[1, 2, ...[3, 4, 5], 6, 7]
```

## Mutabilité

Les foncctions pure en programmation fonctionnelle, ne doivent pas avoir d'effet de bord (side effect). La syntaxe es2015 offre cette fonctionnalité. 

```js 
// Objects
function addMarks( user, marks )
{
	return {
		...user,
		marks
	};
}

const user          = { username: 'eric' };
const userWithMarks = addMarks( user, 20 );

console.log( user, userWithMarks );
```

Pour les tableaux également :

```js
// Arrays
function addUser( users, username )
{
	const user = { username };
	return [
		...users,
		user
	];
}

const user     = { username: 'eric' };
const users    = [ user ];
const newUsers = addUser( users, 'john' );

console.log( users, newUsers );
```

## References

- [Object Literals](https://tutor.mantrajs.com/say-hello-to-ES2015/object-literals)
- [ES6 In Depth: Destructuring](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring/)