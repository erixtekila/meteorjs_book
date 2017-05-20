# Sessions

Les sessions meteor n'ont rien à voir avec les sessions HTTP utilisées pour conserver l'état entre un client et serveur.
**Souvenez-vous, nous sommes connectés sur une websocket persistante !**

Utilité des `Session` :

- juste du côté client
- stockage par clé - valeur
- _in memory_

> **Note** Fonctionne à la façon de `LocalStorage`  

## Définition

```js
Session.set( 'key', value );
```

La sérialisation JSON est permise.


## Valeur par défaut

```js
Session.setDefault( 'key', true );
```

## Lecture

```js
Session.get( 'key' );
```

## Les sessions sont des données reactive

