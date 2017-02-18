# What is this "reactivity" after all ?

## Valeurs réactives natives

- Les curseur des Collection
- Session
- ReactiveVar `meteor add reactive-var`
- ReactiveDict `meteor add reactive-dict`

> **Note** La différence entre une `ReactiveVar` et une `Session`, corespond au fait que cette dernière est globale à l'application. Cf. [A scoped reactivity](https://dweldon.silvrback.com/scoped-reactivity) 

## Exemple d'une valeur reactive personnalisée

> En programmation réactive, lire une valeur revient à s'abonner à des notifications de changement de cette valeur. Il n'est pas nécessaire de déclarer une fonction, ni de l'activer, cela sera fait automatiquement!

>_stephenwalther.com_

_Cf. demos/04custom_reactivity_

## Le fonctionnement en détails

Lorsqu'une valeur reactive est changée, elle notifie automatiquement chaque élément relié. Cela fonctionne comme les tableaux excel, dans lesquels une modification de cellule peut entrainer celles d'autres, automagiquement.

Mais quel est le principe sous-jacent ?
Est-ce que c'est un principe efficace ?


### Function `autorun`

```js
let reactive = new ReactiveVar( 1 );

Tracker.autorun
(
	() =>
	{
		console.log( `autorun reactive : ${reactive.get()}` );
	}
)
```

Si depuis la console, nous modifions la valeur de cette variable, nous observons que cette fonction est activée. 

```js
reactive.set(2); // autorun reactive : 2
```

> **Hint** [Pour activer l'es2015 dans la console, installez l'extension chrome ScratchJS](https://chrome.google.com/webstore/detail/scratch-js/alploljligeomonipppgaahpkenfnfkn)

Quel lien existe t-il entre ces deux valeurs ?

### `Computations`

La fonction `Tracker.autorun()` retourne une valeur, nommée `Computation` dans la terminologie Meteor.

```js
let reactive = new ReactiveVar( 1 );

let computation = Tracker.autorun
(
	() =>
	{
		console.log( `autorun reactive : ${reactive.get()}` );
	}
);

console.log( computation ); // Tracker.Computation{} 
```

![Tracker.Computation methods](../images/Tracker.Computation.png)

Si par exemple, vous utilisez sa méthode `stop()`, plus aucune réactivité n'est active sur la valeur.

### Valeurs réactives personnalisées ?

```js
let reactive = new Tracker.Dependency();

let computation = Tracker.autorun
(
	() =>
	{
		reactive.depend();
		console.log( `autorun reactive called` );
	}
);

reactive.changed();// autorun reactive called
```

### Terminologie

1. Les valeurs réactives sont des `Tracker.Dependency`. Elles émettent leur modification de valeur via leur méthode `changed()`
1. La fonction `Tracker.autorun()` retourne une `Tracker.Computation`. Celle-ci recevra les messages `changed` depuis sa `Tracker.Dependency`
La méthode `Tracker.autorun()` crée un contexte réactif, en créant un objet `Tracker.Computation`, qui sera associé avec la fonction passée à `Tracker.autorun()`
1. Lorsque la méthode `depend()` de la `Tracker.Dependency` est exécutée, elle ajoute l'objet `Tracker.Computation` actuel (grâce à la valeur `Tracker.currentComputation`) à la liste des `Computation` suivies par la `Tracker.Dependency`.
1. Ensuite, toute exécution de la méthode `changed()` de la `Computation` va systématiquement itérer sur tout les objets `Computation` contenus comme dépendance.
1. Lorsque la méthode `invalidate()` de l'objet `Computation` est appelée, la fonction qui lui est associée, sera relancée.

**Ainsi toute fonction passée à `Tracker.autorun()` sera systématiquement relancée dès qu'une de ses `Dependency` est modifiée.**


## Reactivity FAQ

### Est-ce optimisé ?

#### Lien entre la `Dependency` et sa `Computation`

```js
let reactive = new ReactiveVar(1);

let computation = Tracker.autorun
(
	() =>
	{
		console.log( `autorun reactive : ${reactive.get()}` );
	}
);

reactive.dep // Tracker.Dependency
reactive.dep._dependentsById // Object
/* 
{
	54 : Tracker.Computation
}
*/

reactive.dep._dependentsById[ 54 ]._func() //autorun reactive : 1 !!!

reactive.dep.changed() //autorun reactive : 1 !!!
```
Les `Dependency` référencent donc leur `Computation`.

**Dès lors, toutes les `Computation` qui se trouvent dans `dep._dependentsById`, sont systématiquement notifiées, lorsque `changed()` depuis est activé.***

#### `invalidate()` et `Tracker.flush()`

Le cycle de raffraîchissment des dépendances est effectué par une boucle dépendant de l'horloge système 

`window.setInterval( Tracker.flush, 0 )`;

`Tracker.flush()` active le cycle de raffraichissment des dépendances.
 

`invalidate()` permet d'éviter de notifier plusieurs fois pour la même modification de valeur. En effet, elle recquiert que le cycle de dépendance soit relancé, **mais que dans un seul cycle de`Tracker.flush`**.

```js
computation.invalidate();// autorun reactive : 1

computation.invalidate(); computation.invalidate(); computation.invalidate(); // autorun reactive : 1
```

### Reactivity is composition-able !

[Tel que l'évoque cet article](https://www.discovermeteor.com/blog/reactivity-basics-meteors-magic-demystified/), un des comportement intéressant de la réactivité, c'est qu'elle supporte la composition.

> **Hint** La composition est le fait d'envelopper une fonction dans une autre.

```js
let getCount = function ()
{
  return Session.get('count');
};

Template.hello.helpers
({
	counter:()
	{
		console.log('counter helper is running');
		return getCount();
	}
});
```

> **Warning** La composition ne fonctionne que pour les fonctions…

## Références

- [Meteor Reactivity Concepts Explained For Humans](http://www.youtube.com/oembed?url=https://www.youtube.com/watch?v=V8IU-ooJcuI&format=xml)
- [Reactivity basics](https://www.discovermeteor.com/blog/reactivity-basics-meteors-magic-demystified/)
- [Don't do, react](http://stephenwalther.com/archive/2014/12/05/dont-do-react-understanding-meteor-reactive-programming)