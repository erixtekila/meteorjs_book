# Persistance isomorphe

## `Collection`

[ORM](https://en.wikipedia.org/wiki/Object-relational_mapping) vers la base de données mongodb, qui sera étendue dans de futures versions.

## Création

```js
playlist = new Mongo.Collection( "playlist" );
```

> **Note** Vous noterez au passage l'emploi d'une variable globale (pas d'utilisation du mot clé `var`)

## Insertion

```js
playlits_id = playlist.insert
(
	{
		name : "test"
		,urls : []
	}
);
```

## Mise à jour 

```js
playlist.update
(
	{ _id : playlist_id }
	,{
		name : "test2"
	}
);
```

> **Info** Le 1er paramètre correspond à l'identifiant du document.

> **Warning** Utilisez un modificateur pour mettre à jour quelques valeurs du document.

```js
playlist.update
(
	{ _id : playlist_id }
	,{
		$set : { name : "test2" }
	}
);
```

ou plus raccourci :

```js
playlist.update
(
	playlist_id
	,{
		$set : { name : "test2" }
	}
);
```

## Suppression 

```js
playlist.remove( playlist_id );
```