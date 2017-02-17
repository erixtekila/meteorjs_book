# Ajout de logique dans le controller

## Dans `scope`

```javascript
angular.module( 'myApp', [] )
       .controller(
	       'GreetingController', function( $scope )
	       {
		       $scope.now                   = new Date();
		       $scope.helloMessages         = [ 'Hello', 'Bonjour', 'Hola', 'Ciao', 'Hallo' ];
		       $scope.greeting              = $scope.helloMessages[ 0 ];
		       $scope.getRandomHelloMessage = function()
		       {
			       $scope.greeting = $scope.helloMessages[ parseInt( (Math.random() * $scope.helloMessages.length) ) ];
		       }
	       }
       );
```

```html
<body ng-controller="GreetingController">
{{greeting}} Date actuelle <span>{{now | date: 'medium'}}</span>.
<br/>
<button ng-click="getRandomHelloMessage()">Nouveau message de bienvenue</button>
</body>
```

## Règles pour les `controllers`

- Pas de manipulation du DOM. Utiliser les directives à la place.
- Pas de transformation des valeurs des `models`. Utiliser les filtres plutôt.
- Eviter la redondance des fonctions. Utiliser un `service` injecté, il sera partageable qui plus est.

## Propriétés et méthodes dans le `controller`

Angular instancie vos classe en tant que singleton.
Il est possible d'y ajouter des méthodes ou propriétés directement.

```javascript
angular.module( 'myApp', [] )
       .controller(
	       'GreetingController', function( $scope )
	       {
		       this.now                   = new Date();
		       this.helloMessages         = [ 'Hello', 'Bonjour', 'Ola', 'Ciao', 'Hallo' ];
		       this.greeting              = this.helloMessages[ 0 ];
		       this.getRandomHelloMessage = function()
		       {
			       this.greeting = this.helloMessages[ parseInt( (Math.random() * this.helloMessages.length) ) ];
		       }
	       }
       );
```

```html
<body ng-controller="GreetingController as greetingController">
{{greetingController.greeting}} Date actuelle <span>{{greetingController.now | date: 'medium'}}</span>.
<br/>
<button ng-click="greetingController.getRandomHelloMessage()">Nouveau message de bienvenue</button>
</body>
```

> **Info** Exposition du nom de l'instance grâce à `as` dans `ng-controller`
  
`$scope` devrait permettre de séparer les responsabilités des `controllers` et `views`   
Le seul avantage à cette méthode réside l'usage de controllers `imbriqués` ayant des `models` nommés de la même façon.

```html
<div ng-controller='OuterController as outer'>
	<div ng-controller='InnerController as inner'>
          Outer={{outer.someModel}} and inner={{inner.someModel}}
    </div>
</div>
```

> **Note** Il est possible d'utiliser l'héritage prototypal pour que le `controller` interne accède au `$scope` de son parent. 
 
 