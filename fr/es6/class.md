# L'orienté objet en es2015

## Définition

```js
class Vehicle {
	constructor( type, number )
	{
		this.type   = type;
		this.number = number;
	}

	display()
	{
		return `Number: ${ this.number }`;
	}
}

const v1 = new Vehicle( 'Audi', 'GH-2343' );
console.log( v1.display() );
```

## Héritage

```js
class Vehicle {
	constructor( type, number )
	{
		this.type   = type;
		this.number = number;
	}

	display()
	{
		return `Number: ${ this.number }`;
	}
}

class Car extends Vehicle {
	constructor( number )
	{
		super( 'Car', number );
	}

	display()
	{
		const value = super.display();
		return `Car ${value}`;
	}
}

const v1 = new Car( 'GH-2343' );
console.log( v1.display() );
```

> **Note** `super()` permet d'accéder au super constructeur, `super.uneMethode()` à une méthode de la super classe.

## Accesseurs

```js
class Vehicle {
	constructor( type, number )
	{
		this._type   = type;
		this.number = number;
	}

	set type( type )
	{
		this._type = type;
	}

	display()
	{
		return `Number: ${ this.number }`;
	}
}

```
