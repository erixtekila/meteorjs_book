# Structuration des projets

## Chargement des dépendances

### _Lazy loading_

Tout code placé dans le repertoire `imports` sera chargé conditionnellement à son usage. C'est-à-dire que son inclusion sera réalisée uniquement lorsqu'il est utilisé.

**La bonne pratique consiste à inclure tout le code dans ce répertoire.**

### _Eager loading_

A l'inverse, tout code placé en dehors de `imports` sera inclus selon les règles alphanumériques de priorité.

Dès lors, seul deux fichiers devraient être chargé "avec appétit" : 

- `client/main.js`
- `server/main.js`

Ils servent répectivement de point d'entrée de l'application, côté client et serveur. De cette façon, ils importent les dépendances pour lancer l'application.

### scaffolding

Le _scaffolding_ `meteor` permet de créer une hiérarchie optimisée pour démarrer.

```sh
meteor create --full projectname 
```

Tous les dossiers importants seront crées afin de démarrer rapidement un projet.
_Cf. demos/01-full-structure et demos/01-default-structure_


Par contre, pour démarrer depuis un projet vide : 

```sh
meteor create --bare projectname 
```

Pour une aide sur tous les types de projets disponibles :

```sh
meteor create --help
```

## Dossiers spéciaux 

- `imports` Inclusion uniquement via des appels `import from` dans le code
- `node_modules` toutes les dépendances incluses via `npm i --save`
- `client` Disponible uniquement depus le poste client. Toutes les sources sont automatiqment concaténées et minifiées, une fois déployées.
- `server` chargé que sur le serveur. Tout élément qui nedoit pas être partagé avec le client doit impérativement se trouver dedans.
- `public` Tout ce qui est livré tel quel au client. Par exemple, les images, **dont l'URL ne doit pas contenir dans son chemin `public`**.
- `test` uniquement reservé aux tests de l'outil. Chargé nulle part.
