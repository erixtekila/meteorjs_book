# Meteor version 1.4


## Utilisation de l'écosystème node.js

Meteor inclut la version 4 de `node.js`. Ce qui modifie certaines librairies, dont plusieurs sont natives, donc à recompiler selon votre plateforme.

Voir [l'intégration de NPM](npm.md) pour une description sur le découpage des applications en modules.

Bien entendu, cette nouveauté introduit des modifications quant à la hiérarchie des projets `meteor`. [Une explication complète vous attend](../best_practices/structuration.md).

## ES2015

See [Meteor intégration de l'es2015](../intro/README.md)

## New UI frameworks

En plus du moteur de template Spacebar, `meteor` inclus le support de :

- [React.js](https://facebook.github.io/react/)
```sh
npm install --save react react-dom react-addons-pure-render-mixin
```

```js
import React from 'react';
```

La transformation du `jsx` est effectuée par le _transpiler_ babel, inclus depuis le package `ecmascript`.

- [Angular.js](https://angularjs.org/)
Voir [le chapitre dédié](../whats_new/angular.md).

## Mongodb

MongoDB 3.2 et son moteur WiredTiger.
Cela apporte notamment le support du contrôle de la concurrence et une gestion native de la compression.

## Références

- [How to Update Your Enterprise Meteor Application to 1.4](https://blog.meteor.com/how-to-update-your-enterprise-meteor-application-to-1-4-3828b2f946f7?gi=ce0074e2b996)