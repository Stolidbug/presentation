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

### Introduction :

- **Importance de la Gestion des Assets** :
    - La gestion des assets est cruciale car elle impacte non seulement la performance et la vitesse de chargement des
      pages, mais aussi l'expérience utilisateur. Un mauvais management des assets peut entraîner des temps de
      chargement plus longs, des erreurs de rendu et une maintenance plus difficile.

---

- **Webpack Encore** :
    - C'est une interface pour Webpack spécialement conçue pour Symfony, qui permet de gérer les assets de votre projet,
      comme les fichiers JavaScript, les feuilles de style CSS et les images. Il automatise le processus de compilation,
      de minification et d'autres tâches nécessaires pour préparer ces assets pour la production .

---

- **Asset Mapper de Symfony** :
    - C'est une nouvelle composante introduite dans Symfony 6.3 comme une fonctionnalité expérimentale. Elle permet une
      gestion simplifiée des assets, en éliminant la nécessité d'un bundler complexe. Elle exploite les fonctionnalités
      modernes des navigateurs pour gérer les assets directement sans avoir besoin d'un système de build
      supplémentaire .

---

### Webpack Encore :

- **Minification des fichiers** :
    - La minification est le processus de suppression ou de réduction des données inutiles dans un fichier, sans
      affecter la façon dont le navigateur le traite. Cela inclut la suppression des espaces blancs, des commentaires,
      et la réduction des noms de variables, ce qui diminue la taille du fichier et améliore les temps de chargement des
      pages.

---

### Exemple de Minification :

    - Avant la minification, votre fichier `app.js` (500KB) pourrait ressembler à ceci :

```javascript
        function sayHello() {
    console.log('Hello World!');
}

sayHello();
```

    - Après la minification avec Webpack Encore (200KB), il pourrait ressembler à ceci :

```javascript
        function sayHello() {
    console.log('Hello World!')
}

sayHello();
```

---

- **Pré-processing Sass/LESS** :

    - Sass et LESS sont des préprocesseurs CSS qui permettent d'écrire des styles avec plus de fonctionnalités comme les
      variables et les fonctions. Webpack Encore peut compiler ces fichiers en CSS standard que les navigateurs peuvent
      interpréter.

---

### Exemple de Pré-processing Sass/LESS :

- Fichier source : `style.scss`

```scss
        $font-size: 16px;
            body {
              font-size: $font-size;
            }
```

- Fichier compilé : `style.css`

```css
        body {
    font-size: 16px;
}
```

---

- **Support pour React, Vue.js** :
  - Webpack Encore facilite l'intégration de frameworks populaires comme React ou Vue.js dans votre projet Symfony, en
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

- **Hot Module Replacement (HMR)** :

    - Le Hot Module Replacement est une fonctionnalité qui permet de remplacer, ajouter, ou supprimer des modules tout
      en l'application s'exécute, sans nécessité de rafraîchir la page entière. Cela permet une mise au point plus
      rapide en économisant du temps qui aurait été perdu dans le rechargement de la page.

---

### Asset Mapper de Symfony :

- **Exposition des répertoires d'assets** :

    - L'Asset Mapper permet d'exposer des répertoires d'assets en les déplaçant vers un répertoire public, tout en
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

- **Cartographie et Versioning des Assets**:

  - Il identifie et rend accessible publiquement les fichiers dans un répertoire spécifié, comme `assets/`, et versionne ces fichiers pour garantir que les versions les plus récentes sont servies aux utilisateurs .
---

### Exemple de Cartographie et Versioning des Assets :

```twig
     {# templates/base.html.twig #}
     <link rel="stylesheet" href="{{ asset('styles/app.css') }}">
```

---

- **Importmaps**:

  - Les Importmaps sont une fonctionnalité de navigateur qui simplifie l'utilisation de l'instruction import en
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

### Comparaison et Motivation pour le Changement :

- **Simplicité de l'Asset Mapper** :
    - Avec l'Asset Mapper, la configuration est simplifiée et le processus de gestion des assets est plus direct, ce qui
      peut accélérer le développement et réduire la courbe d'apprentissage pour les nouveaux membres de l'équipe.


- **Modernité de l'Asset Mapper** :
    - L'Asset Mapper tire parti des fonctionnalités modernes des navigateurs, comme l'instruction `import` native en
      JavaScript, ce qui permet d'écrire du code plus moderne sans la complexité supplémentaire d'un bundler.

---

### Conclusion : Points Positifs et Négatifs

**Webpack Encore** :

**Points Positifs** :

1. **Polyvalence** : Adapté pour des projets complexes avec des besoins variés en matière de gestion des assets.
2. **Préprocesseurs CSS et Frameworks JS** : Support intégré pour les préprocesseurs CSS et frameworks JavaScript
   modernes.
3. **Hot Module Replacement (HMR)** : Accélère le développement en permettant des mises à jour en temps réel sans
   rechargement complet de la page.

**Points Négatifs** :

1. **Complexité** : Peut devenir complexe, surtout pour ceux qui ne sont pas familiers avec Webpack.
2. **Courbe d'Apprentissage** : Requiert un certain temps d'apprentissage pour une utilisation efficace.

---

**Asset Mapper de Symfony** :

**Points Positifs** :

1. **Simplicité** : Facile à configurer et à utiliser, idéal pour des projets moins complexes.
2. **Modernité** : Exploite les fonctionnalités modernes des navigateurs, permettant un code plus propre et plus
   moderne.
3. **Configuration Minimaliste** : Accélère le développement en réduisant la nécessité de configuration.

**Points Négatifs** :

1. **Fonctionnalités Limitées** : Moins de fonctionnalités par rapport à Webpack Encore, peut ne pas convenir aux
   projets avec des besoins de gestion des assets plus complexes.
2. **Statut Expérimental** : Étant une fonctionnalité expérimentale, il pourrait y avoir des changements futurs ou moins
   de support de la communauté.

---

### Recommandations :

- **Pour les Projets Complexes** : Si votre projet a des besoins complexes en matière de gestion des assets, ou si vous
  avez déjà une configuration bien établie avec Webpack Encore, il pourrait être bénéfique de continuer à l'utiliser.

- **Pour les Nouveaux Projets ou Projets Simples** : Si vous commencez un nouveau projet, ou si votre projet est moins
  complexe, envisagez d'expérimenter avec l'Asset Mapper de Symfony pour simplifier la gestion des assets et accélérer
  le développement.

- **Formation et Support de la Communauté** : Évaluez également la disponibilité des ressources d'apprentissage et le
  support de la communauté pour chacun des outils, cela peut influencer votre décision.
