# Gestion événementielle

## Délégation événementielle

Meteor, tel que jquery, backbone (…), utilise la délégation pour capturer les événements d'interface.
Tous ceux-ci seront disponibles simplement : `click`, `submit` 
  
> **Warning** Utilisez l'arrêt de la propagation `topPropagation()` ou `preventDefault()` pour éviter le changement de page, tel que requis par un `click` sur un lien.  

## Définition

```js
Template.eleves.events
({
  'click' : function () {  },
  'mouseOver, mouseOut' : function () {  }
});
```
## Filtrage

```js
Template.eleves.events
({
  'click .maclasse' : function () {  }
});
```
Uniquement les événements provenant les éléments ayant la classe css.

