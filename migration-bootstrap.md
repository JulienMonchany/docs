# Migration Bootstrap v3 -> v4

## Dependances
### `package.json`
Supprimer la dépendance au framework MAIF
Ajouter la dépendance à Bootstrap 4 

```
npm install bootstrap
```

Vérifier que le fichier contient la dépendance : `"bootstrap": "^4.0.0",`

## `all.scss`
Dans le fichier `all.scss` du projet, remplacer tous les imports du framework maif, et tous les imports relatifs à `bootstrap-sass` 

## `gulpfile.js`
* Modifier la variable `framework: './node_modules/maif-framework-presentation'` par `framework: './node_modules/pfs-presentation-framework'`
*  Supprimer la dépendance à Bootlint qui se base sur la v3 de Bootstrap.
* remplacer `node_modules/bootstrap-sass/assets/javascripts/bootstrap.js` par les scripts ciblés dans la dépendance Bootstrap. Exemple : 
```js
  // Bootstrap dependencies & scripts
  const bootstrapJsPath = 'node_modules/bootstrap/js/dist/';
  var bootstrapJs = [
    'node_modules/jquery/dist/jquery.js', // mandatory
    'node_modules/poper.js/dist/poper.js', 
    bootstrapJsPath + 'util.js', //  mandatory
    bootstrapJsPath + 'modal.js',
    bootstrapJsPath + 'collapse.js',
    bootstrapJsPath + 'tab.js',
  ];
```
Le tableau `bootstrapJs` contient les 3 scripts relatifs au fonctionnement de base de Bootstrap (jquery, popper, util) et les scripts de 3 composants : modal, collapse, tab. 
_Note_: le script popper n'est pas utile à tous les composants, on peut s'en passer. 

Exemple complet :

```js
gulp.task('js-fwk-footer', function () {

  // Bootstrap dependencies & scripts
  const bootstrapJsPath = 'node_modules/bootstrap/js/dist/';
  var bootstrapJs = [
    'node_modules/jquery/dist/jquery.js', // mandatory
    'node_modules/poper.js/dist/poper.js',
    bootstrapJsPath + 'util.js', //  mandatory
    bootstrapJsPath + 'modal.js',
    bootstrapJsPath + 'collapse.js',
    bootstrapJsPath + 'tab.js',
  ];

  // Other JS deps
  const jsScripts = [
    'node_modules/slick-carousel/slick/slick.min.js',
    'node_modules/blazy/blazy.min.js',
    basedir.framework + '/js/*.*',
    basedir.localFramework + '/js/*.*'
  ];

  return gulp.src(bootstrapJs.concat(jsScripts))
    .pipe(cache('js'))
    .pipe(concat('footer.js'))
    .pipe(gulp.dest(basedir.maquette + '/dist/js/rwd'))
    .pipe(browserSync.stream());
});
```
Dans cet exemple on retrouve notre tableau contenant les scripts des composants Bootsrap puis un tableau contenant les scripts hérités du framework PFS et ceux du projet.

# Imports Bootstrap-SASS
`@import 'bootstrap-sass/assets/stylesheets/bootstrap/variables';` devient `@import 'bootstrap/scss/variables';`
`@import "maif-framework-presentation/sass/components/button";` -> `@import 'pfs-presentation-framework/scss/components/button';`
`@import "maif-framework-presentation/sass/components/floating-contact";` -> `@import 'pfs-presentation-framework/scss/components/floating-contact';`
`@import 'maif-framework-presentation/sass/components/lists';` -> `@import 'pfs-presentation-framework/scss/components/lists';`


`$color-00` devient `$black`
`$color-0` devient `$white`

Fonts: variables sont préfixées par `$font`

Media Queries : 
https://v4-alpha.getbootstrap.com/layout/overview/#responsive-breakpoints
`$tablet-media-query` deviennent `@include media-breakpoint-down(md)`
`$tablet-min-media-query` deviennent `@include media-breakpoint-up(md)`

disparition de la mixin `width-height`
disparition des mixins `compass` (utilisation d'un autoprefixer sur le projet)

## Bootstrap
`img-responsive` devient `img-fluid`
remplacer les  `col-center` par une classe `justify-content-center` sur la `row` parente
les classes `col-xs-*` reviennent `col-*`

Les classes `visible-*` et `hidden-*` ont été remplacées, cf. https://getbootstrap.com/docs/4.0/utilities/display/
exemple : `.hidden-xs` devient `.d-none.d-sm-block`, `.visible-xs` devient `.d-block.d-sm-none`

### Forms
les span `input-group-addon` deivennent  des div `input-group-prepend` et  `input-group-append` selon le cas (respectivement avant et après l'input).
Les radios et checkbox sont encadrées dans une div `form-check` au lieu de `form-control`
Messages d'erreurs : suppression de la classe `has-error` sur la div `form-group`, ajout de la classe `is-invalid` sur le `form-control`. la span `help-block` devient une div `invalid-feedback` placée au-dessous de l'input lié.




