# Publication sur mobile

## Ajout des plateformes

### IOS

Nécéssite une machine (virtuelle ou non) qui fait tourner Mac OSX.
Ensuite, il faut installer [Xcode](https://developer.apple.com/xcode/) qui va vous permettre de définir [votre identité et les _provisionning profile_](https://developer.apple.com/library/mac/recipes/xcode_help-accounts_preferences/articles/obtain_certificates_and_provisioning_profiles.html).
Cette procédure est importante pour soumettre votre app sur le store Apple.

```sh
meteor install-sdk ios
meteor add-platform ios
```

### Android

Pour installer les SDK Android :

```sh
meteor install-sdk android
meteor add-platform android
```

## Déploiement sur simulateurs

Pour ouvrir le simulateur Android

```sh
meteor run android
```

et celui IOS

```sh
meteor run ios
```

## Déploiement sur périphérique

L'utilisation sur un smartphone nécessite de permettre les requêtes sur votre adresse IP. Par défaut, [Cordova](https://cordova.apache.org/) nécessite de définir une liste d'adresses autorisées.
A cette fin, créez un fichier `mobile-config.js` à la racine du projet et insérez la ligne suivante

```js
App.accessRule('http://[votre ip]:3000/*');
```

en prenant bien soin de remplacer votre IP !…

Sur Android, il faudra également ajouter [le mode debogage USB](http://developer.android.com/tools/device.html) et démarrer votre serveur ainsi


## Lancement

Android

```sh
meteor run android-device --mobile-server http://192.168.2.123:3000
```

IOS

```sh
meteor run ios-device --mobile-server http://192.168.2.123:3000
```

Cette commande ouvre Xcode afin que vous définissiez le périphérique à connecter.


## Tips & tricks

### viewport

Attetion à bien utiliser un _viewport_ pour mobile

```html
<head>
  <title>mobilapp</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</head>
```

### Offline support

EN ajoutant [le package appcache](http://docs.meteor.com/#/full/appcache), vous pourrez utiliser l'espace de stockage local du client, le [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

- Dès que le visiteur aura consulté pour la prmeière fois l'application, les prochaine visites utiliseront la version mise en cache, avant de contacter le serveur.
- Mise en cache du [hot code push](https://blog.meteor.com/meteor-hot-code-push-with-great-power-comes-great-responsibility-7e9e8f7312d5#.u5h9u6n7r) en tache de fond.
- Mise en cache des éléments pour consultation hors ligne.


La mise en cache peut être aussi activée que sur certains types de périphériques

```js
Meteor.AppCache.config
({
  chrome: false
  ,firefox: false
  ,android : false
  ,chromium : false
  , chromeMobileIOS : false
  , ie : false
  , mobileSafari : false
  , safari : false
});
```

> **Warning** Une limite de 5Mo est à surveiller, car les navigateurs ne disposent pas du même seuil de cache.
Une erreur surviendra sur le serveur, si ce seuil est dépassé.

### Données persistantes

Pour que des valeurs des collections persistent sur le mobile, il est important d'utiliser une solution telle [GroundDB](https://atmospherejs.com/rtnpro/grounddb).

### Intégration au mobile

Cordova propose [plusieurs packages](https://cordova.apache.org/plugins/) pour accéder à la partie hardware du smartphone. Et [MDG certaines intégrations](https://github.com/meteor/mobile-packages)

Par exemple pour des accès à la caméra

```sh
meteor add cordova:cordova-plugin-camera@1.2.0
```

plus dans le `package.js`

```js
 Cordova.depends
 ({
		'cordova-plugin-camera': '1.2.0'
});
```

## Distribution

### Description de l'application

Editez le fichier `mobile-config.js`

```js
App.info
({
  // the bundle ID must be unique across the entire app store
  // usually reverse domains of the creators are used
  id: 'de.yauh.reactivehball',
  version: '1.0.0',
  name: 'ReactiveHBall',
  description: 'The all-knowing H-Ball answers your questions about life',
  author: 'Stephan Hochhaus',
  email: 'stephan@yauh.com',
  website: 'http://yauh.de/building-mobile-apps-with-meteor-the-reactive-h-ball/'
});
```

### Splashscreen et icones

```js
App.icons
({
  // iOS
  'iphone': 'mobile-resources/ios/icon/Icon-60.png',
  // Android
  'android_ldpi': 'mobile-resources/android/icon/drawable-ldpi-icon.png',
});

App.launchScreens({
  // iOS
  'iphone': 'mobile-resources/ios/splash/Default~iphone.png',
  // Android
  'android_ldpi_portrait': 'mobile-resources/android/splash/drawable-port-ldpi-screen.png',
});
```

### Publication

```sh
meteor build --server=http://votre.serveur.com ../build
```

### Soumission à Google Play

Tout d'abord avoir une compte développeur google.

1- Création d'une clé, essentielle à toute mise à jour

```sh
keytool -genkey -alias nom_de_l_app -keyalg RSA -keysize 2048 -validity 10000
```

à sauvegarder

```sh
keytool -exportcert -alias nom_de_l_app -file nom_de_l_app.cer
```

2- Signature de la publication meteor

```sh
jarsigner -digestalg SHA1 unaligned.apk nom_de_l_app
```

Puis "alignement" de votre application

```sh
~/.meteor/android_bundle/android-sdk/build-tools/21.0.0/zipalign 4 unaligned.apk production.apk
```

3- Dernière étape : uploader le fichier `production.apk` sur [la developer console de Google](https://play.google.com/apps/publish/).


### Soumission à l'itunes store

1- Posséder un compte développeur Apple.

2- Puis configurer votre _provisionning profile_. Cela correspond probablement à la procédure d'alignement nécessaire pour Android.

3- Suivre [ce tutorial pour configurer votre soumission d'application](http://codewithchris.com/submit-your-app-to-the-app-store/)


## Références

- [Mobile chapter, Meteor guide](https://guide.meteor.com/mobile.html)
- [The illustrated guide to mobile apps with Meteor](http://yauh.de/index.html%3Fp=392.html)
- [A Beginners Guide to Mobile Development with Meteor](https://www.sitepoint.com/beginners-guide-mobile-development-meteor/)
