# Injection de dépendance et minification
 
 Dans la mesure ou Angular détermine les références injectées au `controller` grâce à leur nom, il est important de définir une approche en cas de publication minifiée.
 Deux solutions existent :
 
 ## $inject
 
 ```javascript
function DemoController( $rootScope, $scope, $http )
{
};

DemoController.$inject = [ '$rootScope', '$scope', '$http' ];
angular.module( 'myApp', [] )
       .controller( 'DemoController', DemoController ); 
 ```
 
## à la déclaration du `controller`

```javascript
angular.module( 'myApp', [] )
       .controller(
	       'DemoController', [
		       '$rootScope', '$scope', '$http'
		       , function( $rootScope, $scope, $http )
		       {
		       }
	       ]
       );
```

> **Warning** L'ordre des arguments est essentiel.