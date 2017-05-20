# Minimongo

Principe #3 _Data evrywhere_.

- Même syntaxe que côté serveur.
- Si la collection existe côté serveur, elle sera synchronisée automatiquement.
- [Système PubSub](https://en.wikipedia.org/wiki/PubSub)

> **Warning** Contrairement au serveur, qui utilise la [librairie Fibers](https://www.npmjs.com/package/fibers), une syntaxe asynchrone est nécessaire :

```js
playlist.insert
(
	{ name : "playlist_fom_client", urls : [] }
	, function( err, res )
	{
		var playlist_id = res;
	}
);
```

Pour effectuer une recherche dans une collection cliente (depuis la console de l'inspecteur web par exemple) :

```js
playlist.findOne( { name : "test" } );
```