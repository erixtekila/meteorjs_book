# Sujets avancés

## Les _watcher_

**Les _watchers_ observent et réagissent aux modifications des modèles.**

Utilisez `$scope.$watch()` afin de suivre ces évolutions.

[watcher](http://jsbin.com/detomi/edit?html,js,output)

> **Note** Les _watchers_ sont toujours notifié une fois, dès le démarrage de l'application. Il est possible de connaître cet état en comparant les valeurs passées en paramètres au callback.  

<!-- Force new blockquote -->

> **Hint** La méthode `$watch()` retourne une fonction, permettant le désabonnement.
 
```javascript
var unwatch = $scope.watch( 'wishListCount',function (newValue,oldValue){ } ) )
// time pass...
unwatch();
```

## `$watchCollection()`

Permet d'obtenir un callback lors de la modification d'une des propriétés d'un object ou d'un array.
 
## Le cycle `$scope.$apply()` et `$rootScope.$digest()`

La notification de changement d'une expression du DOM (\{\{\}\}) s'effectue grâce à une fonction `$watch()` enregistrée lors de l'analyse du code HTML.

Toutefois, comment Angular fait-il pour savoir qu'une valeur de `ng-model` a été modifiée ?
Est-ce grâce à une boucle de vérification continue ? Non, bien heureusement !
   
`$scope` dispose d'une méthode `$apply()` qui prend une fonction comme paramètre. **Toute mutation d'un modèle doit avoir lieu dans cette méthode.** Sans quoi Angular ne peut mettre à jour les expressions reliées. 

Lorsqu'une fonction `$apply()` est utilisée, automatiquement **`$rootScope.digest()` va lancer un cycle de propagation des changements aux portées enfants**.

> **Warning** Ce cycle peut engendrer des modifications en cascade. Le cycle de `$digest()` sera invoqué jusqu'à ce que toutes les propagations auront eu lieu.
 
<!-- blockquote force -->
 
> **Warning** Evitez d'éffectuer des modifications de modèles dans les callbacks de `$watch()`…

<!-- blockquote force -->

> **Hint** Il est possible de savoir lorsqu'un cycle `$digest()` est activé. Pour cela, abonnez une fonction, comme seulm argument de `$watch()`
   
```javascript
$scope.$watch
(
	function()
	{
        console.log('En plein cycle de digestion !');
        return;
	}
);
```

Vous comprenez désormais que lorsque vous utilisez des directives natives telles que `ng-click` ou `ng-model`, en interne le cycle des `$digest()` est invoqué.

## Un `$digest()` par l'exemple

Tachez de corriger ce code.

[Digest cycle](http://jsbin.com/bocopo/1/edit?html,js,output)

Réponse : la valeur de message ne sera mise à jour que si `$apply()` est utilisé, car angular ne peut suivre la modification de la valeur `message` depuis `scheduleTask()`. 

[Digest cycle fixed](http://jsbin.com/yenuvo/1/edit?html,js,output)

> **Note** La bonne pratique est d'appeler `$apply()` sans argument, afin de lancer la propagation des changements. 