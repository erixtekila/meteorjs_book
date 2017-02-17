# Provider

Le plus configurable de tous les services.
Example : `$route` cha,ge de comportement selon la propriété `html5Mode`.

**Les `providers` peuvent être injectés dans l'appel à `config()`**

```javascript
angular.module( 'myApp' )
       .provider(
	       'greet', function()
	       {
		       this.greeting = 'Hello';
		       //we can configure this.
		       // The default is Hello.
		       this.$get        = function()
		       {
			       //this will be called to obtain greet service
			       var greeting = this.greeting;
			       return function( name )
			       {
				       alert( greeting + ', ' + name );
			       }
		       }
		       this.setGreeting = function( greeting )
		       { //setter for greeting text
			       this.greeting = greeting;
		       }
	       }
       );
```

> **Hint** Tous les `services` disposent d'un `provider` automatiquement.

```javascript
angular.module('myApp').config(function(greetProvider) { // inject the provider
  greetProvider.setGreeting('Tcho'); //configure our provider
});
angular.module('myApp').controller('TestController', function(greet) {
  greet('Eric');
});
```

> **Note** Angular ajoute le suffixe "Provider". C'est ainsi qu'il est retrouvé dans la méthode `config()`.