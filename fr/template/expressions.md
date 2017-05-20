# Logique dans les templates

> **Note** Les bonnes pratiques indiquent qu'il vazut mieux éviter de mélanger code et affichage. Toutefois, pour des usages moindres, il est intéressant de pouvoir intervenir depuis le moteur de template sur les valeurs à afficher.

## Conditions

```js
{{#if condition}} ... {{else}} ... {{/if}}
```

## Portée au sein des objets

Lorsqu'un helper retourne un objet, il est possible d'utiliser la notation pointée au sein du template.

Toutefois, grâce à une expression `{{#with}}`, le contexte d'évaluation sera définie pour la référence passée :       

```js
{{#with object}}
   {{ property }}
{{/with}}   
```

## Boucles

### `object`

L'expression `{{#each list}}` crée une itération et met dans la portée de l'objet.

### `array`

```js
Template.days.helpers({
  days_name: ["Lun", "Mar", "Mer", "Jeu", "Ven", "Sam", "Dim"]
});
```

`{{this}}` retourne l'élément en cours d'itération.

```html
<template name="days">
  <ul>
  {{#each days_name}}
    <li>{{this}}</li>
  {{/each}}
  </ul>
</template>   
```   

> **Note** {{@index}} retourne l'index en cours.
