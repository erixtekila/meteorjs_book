# Les `directives`

Les directives proposent d'enrichir le HTML de nouveaux éléments ou attributs.
`ng-repeat` est une directive native par exemple.

Le framework vous permet ainsi de composer vos propres éléments.

## Directive simple

```javascript
angular.module('myApp', []).directive('helloWorld', function() {
  return {
      restrict: 'AEC',
      replace: true,
      template: '<h3>Hello, World!</h3>'
}; });
```

Votre code peut exposer désormais soit

- `<hello-world>`
- `<div hello-world>`
- `<div data-hello-world></div>`, plus proche du HTML5

## `restrict`

La propriété `restrict` définie quel type de syntaxe HTML est permise.
Ainsi, "AEC" équivaut à attribut, élément ou classe.  

## `template`

Le format HTML de sortie.
Il peut être fait usage de templateURL pour définir un template défini dans un fichier distant.
 
## `replace`

Subtitue le template à l'élement.