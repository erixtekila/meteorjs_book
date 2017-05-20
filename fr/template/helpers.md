# Template helpers

Les helpers définissent soit des valeurs, soit des fonctions renvoyant des données.
**Leur but consiste à faire le lien entre les données et les templates.**
 
  
## Convention de nommage
 
`Template` contient une référence à tous les templates.

Par convention, toutes les propriétés passées en paramètre d'un objet associatif de la fonction helpers du template ciblé, deviennent disponibles comme données :

```js
Template.playlist_tpl.helpers
(
	{
		urls : [ "https://www.youtube.com/embed/dpmXyJrs7iU" ]  	
	 }
);
```

ou 

```js
Template.playlist_tpl.helpers
(
	{
		getUrls : function()
		{
		 	return [ "https://www.youtube.com/embed/dpmXyJrs7iU" ];
		}
	 }
);
```