# <div class="center-text">Gestion des Assets dans Symfony avec Asset Mapper ou Webpack Encore </div>

---

### Sommaire

1. **<span class="important">Introduction</span>**


2. **<span class="important">Webpack Encore</span>**


3. **<span class="important">Asset Mapper de Symfony</span>**


4. **<span class="important">Comparaison et Motivation pour le Changement</span>**


5. **<span class="important">Conclusion : Points Positifs et Négatifs</span>**


6. **<span class="important">Recommandations</span>**

   
---
class: center, middle
### Introduction :
---
class: center, middle
#### Importance de la Gestion des Assets :
    La gestion des assets est cruciale car elle impacte non seulement la performance et la vitesse de chargement des
      pages, mais aussi l'expérience utilisateur. Un mauvais management des assets peut entraîner des temps de
      chargement plus longs, des erreurs de rendu et une maintenance plus difficile.

---
class: center, middle
#### Webpack Encore :
    C'est une interface pour Webpack spécialement conçue pour Symfony, qui permet de gérer les assets de votre projet,
      comme les fichiers JavaScript, les feuilles de style CSS et les images. Il automatise le processus de compilation,
      de minification et d'autres tâches nécessaires pour préparer ces assets pour la production .

---
class: center, middle
#### Asset Mapper de Symfony :
    C'est un nouveau composant introduit dans Symfony 6.3 comme une fonctionnalité expérimentale. Il permet une
      gestion simplifiée des assets, en éliminant la nécessité d'un bundler complexe. Il exploite les fonctionnalités
      modernes des navigateurs pour gérer les assets directement sans avoir besoin d'un système de build
      supplémentaire .

---
class: center, middle

### Webpack Encore :
---
class: center, middle
#### Minification des fichiers :
    La minification est le processus de suppression ou de réduction des données inutiles dans un fichier, sans
      affecter la façon dont le navigateur le traite. Cela inclut la suppression des espaces blancs, des commentaires,
      et la réduction des noms de variables, ce qui diminue la taille du fichier et améliore les temps de chargement des
      pages.

---

### Exemple de Minification :

    - code expansé, `app.js` (500KB) :

```javascript
    function sayHello() {
        console.log('Hello World!');
}

sayHello();
```

    - minifié `app.js` (200KB) :

```javascript
    function sayHello(){console.log('Hello World!')}sayHello();
```


---
class: center, middle
#### Pré-processing Sass/LESS :

    Sass et LESS sont des préprocesseurs CSS qui permettent d'écrire des styles avec plus de fonctionnalités comme les
      variables et les fonctions. Webpack Encore peut compiler ces fichiers en CSS standard que les navigateurs peuvent
      interpréter.

---

### Exemple de Pré-processing Sass/LESS :

**Fichier source Sass (`style.scss`):**

```scss
$font-size: 16px;
$primary-color: #333;

@mixin theme($color) {
  color: $color;
  background-color: lighten($color, 40%);
}

body {
  font-size: $font-size;
  @include theme($primary-color);
}
```

---

**Fichier compilé CSS (`style.css`):**

```css
body {
  font-size: 16px;
  color: #333;
  background-color: #f2f2f2;
}
```
---
class: center, middle
#### Support pour React, Vue.js :
    Webpack Encore simplifie l'intégration de frameworks populaires comme React ou Vue.js dans votre projet Symfony, en
        gérant la configuration nécessaire pour compiler et servir ces assets.

---

### Exemple de Support pour React, Vue.js:

- Configuration de Webpack Encore pour Vue.js :
     ```javascript
     // webpack.config.js
     const Encore = require('@symfony/webpack-encore');

     Encore
         .setOutputPath('public/build/')
         .setPublicPath('/build')
         .enableVueLoader();

     module.exports = Encore.getWebpackConfig();
     ```

---
class: center, middle

#### Hot Module Replacement (HMR) :

    Le Hot Module Replacement est une fonctionnalité qui permet de remplacer, ajouter, ou supprimer des modules tout
    en l'application s'exécute, sans nécessité de rafraîchir la page entière. Cela permet une mise au point plus
    rapide en économisant du temps qui aurait été perdu dans le rechargement de la page.

---
class: center, middle
### Asset Mapper de Symfony

---
class: center, middle
### Exposition des répertoires d'assets :

    L'Asset Mapper permet d'exposer des répertoires d'assets en les déplaçant vers un répertoire public, tout en
      versionnant les noms de fichiers pour éviter les problèmes de cache.

---

### Exemple d'Exposition des répertoires d'assets :

```yaml
        #config/packages/asset_mapper.yaml
        asset_mapper:
          directories:
            - '%kernel.project_dir%/assets'
 ```

---
class: center, middle
#### Cartographie et Versioning des Assets:

Il identifie et rend accessible publiquement les fichiers dans un répertoire spécifié, comme `assets/`, et versionne ces fichiers pour garantir que les versions les plus récentes sont servies aux utilisateurs .
---

### Exemple de Cartographie et Versioning des Assets :

```twig
     {# templates/base.html.twig #}
     <link rel="stylesheet" href="{{ asset('styles/app.css') }}">
```

---
class: center, middle
#### Importmaps:

    Les Importmaps sont une fonctionnalité de navigateur qui simplifie l'utilisation de l'instruction import en
        JavaScript, permettant d'importer des modules sans nécessiter un système de build. L'Asset Mapper peut générer une
        Importmap pour votre projet, facilitant ainsi la gestion des dépendances JavaScript .

---

### Exemple d'Importmaps :

```json
        {
  "imports": {
    "bootstrap": "/assets/bootstrap-5.0.0/dist/js/bootstrap.min.js"
  }
}
```

---
class: center, middle
### Comparaison et Motivation pour le Changement :

#### Simplicité de l'Asset Mapper :
    Avec l'Asset Mapper, la configuration est simplifiée et le processus de gestion des assets est plus direct, ce qui
      peut accélérer le développement et réduire la courbe d'apprentissage pour les nouveaux membres de l'équipe.

---
class: center, middle
#### Modernité de l'Asset Mapper :
    L'Asset Mapper tire parti des fonctionnalités modernes des navigateurs, comme l'instruction `import` native en
      JavaScript, ce qui permet d'écrire du code plus moderne sans la complexité supplémentaire d'un bundler.

---
class: center, middle
### Conclusion : Points Positifs et Négatifs
---
class: center, middle
#### Webpack Encore :
👍 Polyvalence, support pour préprocesseurs CSS et frameworks JS, HMR.<br>
👎 Complexité et courbe d'apprentissage.

---
class: center, middle
#### Asset Mapper de Symfony :
👍 Simplicité, modernité, configuration minimale.<br>
👎 Fonctionnalités limitées, statut expérimental.

---
class: center, middle
### Recommandations :

Choisissez Webpack Encore pour des projets complexes ou continuez son utilisation si déjà en place. Considérez l'Asset Mapper pour des projets nouveaux ou moins complexes, en tenant compte des ressources d'apprentissage et du support de la communauté.


