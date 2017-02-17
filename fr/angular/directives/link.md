# La fonction `link`

Utilisée lorsqu'un directive doit accéder à `$scope` :

- pour défnir des `models` dans le _scope_
- pour le `$watch()` de `models`
- pour l'ajout d'observateurs DOM

[Fonction link](http://jsbin.com/poluse/edit?output)

```javascript
angular.module('myApp', []);
angular.module('myApp').controller('MainController', function($scope) {
  $scope.message = 'I love AngularJS';
});
```

```javascript
angular.module( 'myApp' )
       .directive
       (
	       'helloWorld', function()
	       {
		       return {
			       restrict: 'AEC',
			       replace : true,
			       template: '<p ng-click="clearMessage()">Hello, World! {{ message }}</p>',
			       link    : function( scope, elem, attrs )
			       {
				       scope.$watch(
					       'message', function( value )
					       {
						       console.log( 'Message Changed!' );
					       }
				       );
				       scope.clearMessage = function()
				       {
					       scope.message = '';
				       };
				       // I use jQuery-lite to register my listener !
				       elem.bind(
					       'mouseover', function()
					       {
						       elem.css( 'cursor', 'pointer' );
					       }
				       );
			       }
		       };
	       }
       );
```

```html
<body ng-controller="MainController">
  <input type="text" ng-model="message" placeholder="Enter message" /> <hello-world></hello-world>
</body>
```

