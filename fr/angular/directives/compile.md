# La fonction `compile`
 
Utilisée pour effectuer des transformations avant que le fonction `link` ne soit activée.

```javascript
angular.module('testModule').directive('testDirective', function() {
  return {
    compile: function(tElem,attrs) {
      //do optional DOM transformation here
      //tElem is jQLite/jQuery wrapped
      return function(scope,elem,attrs) {
        //linking function here
      };
} };
});
```
