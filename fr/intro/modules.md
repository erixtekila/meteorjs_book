# Gestion des dépendances

Meteor dispose de deux gestionnaires de dépendances.
Le premier, [Atmosphere](https://atmospherejs.com/) permet aux développeurs de partager des modules isomorphes. Celui-ci est inclus avec `meteor` depuis sa création. Il est décrit dans ce chapitre.

Le second provient de l'ajout de l'es2015 dans le framework. Une explication détaillée est disponible au chapitre [Modularité NPM](../whats_new/npm.md).

>**Hint** Il est tout à fait possible d'utiliser les deux systèmes au sein d'un même projet.

## Ajouter un paquet

```sh
meteor add package-name
```

## Supprimer un paquet

```sh
meteor remove package-name
```

## Lister les paquets installés

```sh
meteor list

autopublish      1.0.2  Publish the entire database to all clients
insecure         1.0.2  Allow all database writes by default
meteor-platform  1.2.1  Include a standard set of Meteor packages in your app
```

>**Hint** Une liste des dépendances atmosphere est également disponible dans le fichier `.meteor/packages`.

## Package registry

[Atmosphere](https://atmospherejs.com/)… est-ce que j'ai une gueule d'atmosphère ?
