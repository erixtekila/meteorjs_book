# Curseurs réactifs

Les curseurs réactifs correspondent à un principe de la [programmation fonctionnelle reactive](https://en.wikipedia.org/wiki/Reactive_programming). 

Si une donnée est gérée par un **contexte réactif**, est modifiée, son contexte sera invalidé. Cela provoquera un événement de mise à jour.

Par exemple : 

```js
playlist.find().fetch();
```

- La méthode `find()` retourne un [curseur réactif](http://docs.meteor.com/#/full/mongo_cursor)
- `fetch()` est une méthode de `Mongo.Cursor` qui permet d'obtenir la liste des valeurs de la collection.

> **Warning** Un curseur utilisé ne contient plus de valeurs, il faudra le renouveler avec `rewind()`
