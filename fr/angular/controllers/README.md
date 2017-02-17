# Controllers

**Le role des `controllers` est d'ajouter à la vue des modèles ou fonctions, via leur `scope`**

La liaison entre la déclaration HTML et le constructeur du `controller` s'établie grâce à l'attribut `ng-controller='LoginController'`
 
```javascript
angular.module( 'myApp', [] )
       .controller(
	       'GreetingController', function( $scope )
	       {
		       $scope.now = new Date(); //set the model 'now' on scope
		       $scope.greeting = 'Hello';    //set the name model on scope
	       }
       );
```

> **Note** Notez l'usage de l'argument `$scope` passé en paramètre. Il s'agit d'une **injection de dépendance**, pont avec la partie graphique HTML. 

```html
<body ng-controller="GreetingController">
  {{greeting}} Il est <span>{{now | date:'medium'}}</span>
</body>
```
> **Hint** Il est également possible de se servir de `$rootScope` pour obtenir une référence globale.

Chaque fois qu'un attribut `ng-controller` est trouvé, une portée `scope` est créee et rendue disponible au `controller` 

> **Note** Notez l'usage du filtre `date` au sein de l'expression `{ {now | date:'medium'} }`
