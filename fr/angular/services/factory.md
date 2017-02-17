# Les _factory_

Les `factory` sont d'autres valeurs injectables. Il s'agit de "configurateurs de services".
 
```javascript
angular.module('myApp').factory('helloService',function(){
  return {
    sayHello: function(name){
      console.log('Hello '+name);
    },
    echo: function(message){
      console.log(message);
    }
} }); 
``` 

```javascript
angular.module('myApp').controller('TestController', function(helloService) {
  helloService.sayHello('Mediabox');
  helloService.echo('I Love Mediabox');
});
``` 

> **Hint** We are Singleton also !
