# Bonnes pratiques

## Principe de la modularisation par fonctionnalités

- `app.js`
- `controller.js`
- `directives.js`
- `filter.js`
- `services.js`

## Principe de la modularisation par couches

```
/app
    /img -- application level images
    /css -- application level css
    /js
        app.js -- the main app module
    /modules
		/login
			/js
				controllers.js  --controllers for login module
                directives.js   --directives for login module
            /views -- views for login module
            /css
            /img
            loginModule.js -- Main login module definition
        /comment
            /js
                controllers.js  --controllers for login module
                directives.js   --directives for login module
            /views -- views for comment module
            /css
            /img
            commentModule.js -- Main comment module definition
        
    index.html
```

dans le fichier `/app/modules/login/js/controllers.js` on déclare par exemple

```javascript
angular.module('mainApp.login.controllers',[]);
```

et dans `/app/modules/login/loginModule.js`

```javascript
angular.module
(
  	'loginModule'
  	,[
  		'mainApp.login.controllers'
  		, 'mainApp.login.directives'
  	]
);
```

Pour finir, l'`index.html` défini un attribut `ng-app='mainApp'` et `/app/app.js` les deux dépendances

```javascript
angular.module('mainApp',['loginModule','commentModule']);
```

> **Note** La notation des noms de module mime la structuration en package d'autres environnements. Il s'agit juste d'une convention, non d'une obligation.