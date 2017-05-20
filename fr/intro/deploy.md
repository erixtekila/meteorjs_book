# Easy deploy

Les applications meteor utilisent node.js et mongodb de façon standard : principe #6.

### Déploiements `meteor.com`

Offre payante (0,04$/h) utilisant la plateformme PAAS (_platform-as-a-service_), soit le cloud meteor.

```sh
meteor deploy app.meteor.com
```

Création d'un compte nécessaire :

```sh
meteor login
```

### Déploiement sur hébergement dédié

```sh
meteor build --directory
```

Crée une archive pour le déploiement sur un serveur dédié.
A l'intérieur, un fichier `README` vous conduit sur les étapes à suivre.

> This is a Meteor application bundle. It has only one external dependency:
Node.js 0.10.33 or newer. To run the application:

> ```sh
  $ (cd programs/server && npm install)
  $ export MONGO_URL='mongodb://user:password@host:port/databasename'
  $ export ROOT_URL='http://example.com'
  $ export MAIL_URL='smtp://user:password@mailhost:port/'
  $ node main.js
```

> Use the PORT environment variable to set the port where the
application will listen. The default is 80, but that will require
root on most systems.

> Find out more about Meteor at meteor.com.


> **Note** Vous avez une application node.js "standard".

> **Hint** Une mise en production nécessite les gestion de processus tels que [forever](https://github.com/nodejitsu/forever) ou [pm2](https://github.com/Unitech/pm2)

### Déploiements pour mobile

Cerise sur le gateau…

```sh
meteor --help add-platform
Usage: meteor add-platform <platform> [platform..]

Adds platforms to your Meteor project. You can add multiple
platforms with one command.

Available platforms:
  server
  browser
  android
  ios (on OS X only)

Currently, the server and browser platforms are present in every
Meteor project and cannot be removed.
````
