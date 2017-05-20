# Spacebars, un moteur de template

Syntaxe très proche des template classiques, comme [Handlebars](http://handlebarsjs.com/) :

```html
<div>{{ name }}</div>
```

ou encore 

```html
<div data-{{attr}}={{value}}></div>
```

## Définition 

Tous les templates sont définis entre les balises `<template>` et diovent avoir unattribut `name`.

```html
<template name="name_tpl">
	<div>{{ name }}</div>
</template>
```

## _Partials_

L'inclusion des templates se fait grâce à la syntaxe `{{> name_tpl}}`.

## Templates spéciaux

Les templates `<body>` et `<head>` seront automatiquement inclus dans la sortie html.
  
## Logique

La syntaxe pour inclure des blocs logiques `{{#if}}...{{/if}}` ou encore `{{#each playlist}}...{{/each}}`.

## Structuration 

Ils peuvent soit être définis dans un seul fichier ou en externe.
Exemple de l'application de démonstration leaderboard : 

```html
<head>
  <title>Leaderboard</title>
  <meta name="viewport" content="width=device-width, user-scalable=no">
</head>

<body>
  <div id="outer">
    {{> leaderboard}}
  </div>
</body>

<template name="leaderboard">
  <div class="leaderboard">
    {{#each players}}
      {{> player}}
    {{/each}}
  </div>

  {{#if selected_name}}
  <div class="details">
    <div class="name">{{selected_name}}</div>
    <input type="button" class="inc" value="Give 5 points" />
  </div>
  {{else}}
  <div class="none">Click a player to select</div>
  {{/if}}
</template>

<template name="player">
  <div class="player {{selected}}">
    <span class="name">{{name}}</span>
    <span class="score">{{score}}</span>
  </div>
</template>
```