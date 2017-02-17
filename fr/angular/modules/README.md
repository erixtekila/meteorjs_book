# Les modules

Les modules sont le moyen de créer une application modulaire pour angular.
Il existe des modules livrés avec le framework, tels que ceux préfixés par `ng` 

```javascript
// Declaration with 2 arguments
angular.module( 'firstModule', [] ); // no dependencies
angular.module( 'firstModule', [ 'moduleA', 'moduleB' ] ); // 2 dependencies

// Get the reference module as return value
var firstModule = angular.module( 'firstModule', [] ); //define a module
// Register a controller to the module
firstModule.controller(
	'FirstController', function( $scope )
	{
		//
	}
);

// Register a directive
firstModule.directive(
	'FirstDirective', function()
	{
		return {};
	}
);
``` 

Afin d'éviter de polluer l'espace global
 
```javascript
(function()
{
	var firstModule = angular.module( 'firstModule', [] );
	
	firstModule.controller(
		'FirstController', function( $scope )
		{
		}
	);
	firstModule.directive(
		'FirstDirective', function()
		{
			return {};
		}
	);
})();
```

ou mieux, `module( "modulename" )` retourne une réference au module 

```javascript
// Dependency list
angular.module( 'firstModule', [] );
// Chaining
angular.module( 'firstModule' )
       .controller(
	       'FirstController', function( $scope )
	       {
	       }
       );
angular.module( 'firstModule' )
       .directive(
	       'FirstDirective',
	       function()
	       { 
		       return {
	           };
			}
       );
```

> **Warning** Attention de ne pas déclarer plusieurs fois un module avec le même nom.

Via le chainage

```javascript
angular.module( 'firstModule', [] )
       .controller(
	       'FirstController', function( $scope )
	       {
		       //your rocking controller
	       }
       )
       .directive(
	       'FirstDirective', function()
	       { //your directive
		       return {};
	       }
       );
``` 

  
> **Note** Le nom du module permet d'y faire référence depuis n'importe quel fichier.   