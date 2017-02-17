# Vues multiples et _router_

Angular supporte les [_Single Page Application_](https://en.wikipedia.org/wiki/Single-page_application).
De plus, la séparation des états de notre webapp en plusieurs vues, offre une modularité apréciable.
 
Le principe consiste à associer une URL à un état de notre application.
Généralement, un _router_ convoque un template, un `controller` par route. 

## `ng-route`

> **Warning** Attention de bien ajouter le fichier `angular-route.js` qui n'est pas inclus par défaut.

Séparons les vues en _partials_ :

```javascript
angular.module( 'myApp' )
       .config(
	       function( $routeProvider )
	       {
		       $routeProvider.when
		       (
			       '/view1'
			       , {
				       controller : 'Controller1',
				       templateUrl: 'partials/view1.html',
			       }
		       )
				.when(
				 '/view2', {
				     controller : 'Controller2',
				     templateUrl: 'partials/view2.html',
				 }
				);
	       }
       );
```

> **Tag** /demos/03-router

Version HTML5 avec `history.puyshState()`

> **Tag** /demos/03-router_pushState

