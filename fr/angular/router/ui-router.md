# `ui-router`

`ng-router` n'est pas parfait. Par exemple, les vues imbriquées ne sont pas supportées.

** `ui-router` utilise une approche basée sur les états plutôt que les URLs.**

> **Tag** /demos/05-ui-router

Chaque état est représenté par une URL, une URL de template et un `controller`.

## Les vues imbriquées

Pour les vues imbriquées, `ui-router` introduit une notation pointée :

```javascript
$stateProvider

    // HOME STATES AND NESTED VIEWS ========================================
    .state('home', {
        url: '/home',
        templateUrl: 'partial-home.html'
    })

    // nested list with custom controller
    .state('home.list', {
        url: '/list',
        templateUrl: 'partial-home-list.html',
        controller: function($scope) {
            $scope.dogs = ['Bernese', 'Husky', 'Goldendoodle'];
        }
    })

    // nested list with just some random string data
    .state('home.paragraph', {
        url: '/paragraph',
        template: 'I could sure use a drink right now.'
    })

```

Etat qui sera accessible depuis 

```html
<a ui-sref=".list" class="btn btn-primary">List</a>
```