# Les services

Les services encapsulent une logique et exposent une API.
Ils permettent de défnir des comportements distribués entre les `controllers`.
 
Angular dispose de services natifs tels que `$http` ou `$timeout`.

> **Note** Les services sont des singleton, ils disposent ainsi d'un accès global et unique.
  
```javascript
angular.module('myApp').service('helloService',function(){
  this.sayHello=function(){ // define an instance method
    alert('Hello Mediabox, à vot\' service !');
  }
});  
```
Le serbice devient disponible dans les `controllers`, par injection.

```javascript
angular.module( 'myApp' )
       .controller(
	       'TestController', function( helloService )
	       {
		       helloService.sayHello(); //
	       }
       );
```

> **Hint** Les services sont toujours activés à chaud (_lazy instanciation_). POur forcer leur initialisation, passez leur nom comme dépendance de `$module( "app" ).$run()`

```javascript
angular.module('myApp').run(function(helloService){
    //Initialisation forcée
});
```