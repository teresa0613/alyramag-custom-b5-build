# Alyra Bootstrap Challenge - Custom Bootstrap5 CSS build

## Prérequis : `node` et `npm` sont installés

## Step 0

Créer un dossier `custom` dans la racine du projet `alyra-challenge-custom-b5`

```bash
mkdir custom
```

Dans le dossier `custom` créer le fichier `mybootstrap.scss`

```bash
touch custom/mybootstrap.scss
```

---

## Step 1

Nous allons installer bootstrap depuis [npm](https://www.youtube.com/watch?v=ZNbFagCBlwo)

Dans le terminal lancer la commande `npm init`

```bash
npm init
```

La ligne de commande posera quelques questions, les réponses seront intégrées dans un nouveau fichier qui va se créer (tout seul) - `package.json`.

Pour l'instant les valeurs par défaut sont tout à fait ok, attention au "name" de votre projet - il doit être en minuscules, sans espaces, peut contenir "-" ou "\_".

Le fichier `package.json` est un fichier très important, une sorte d'identifiant de projet et de son manifeste. Plus d'info [ici.](https://docs.npmjs.com/creating-a-package-json-file)

Avant que nous passons à l'installation du bootstrap depuis npm, on devrait s'assurer d'avoir `node_modules` dans le fichier `.gitignore`. `.gitignore` spécifie les fichiers et/ou repertoires qui devraient pas être trackés par git.

Si votre projet ne contient pas de fichier `.gitignore` vous pouvez le créer dans la racine du projet

```bash
touch .gitignore
```

Voici un exemple de son contenu

```
.DS_Store
node_modules
```

Passons maintenant à l'installation de bootstrap, et plus précisement sa version 5.0.0-alpha

```bash
npm install --save-dev bootstrap@next
```

Des nouveaux dossiers et fichiers apparaissent 💫

```bash
├── node_modules
│   ├── bootstrap
│   │   ├── LICENSE
│   │   ├── README.md
│   │   ├── dist
│   │   │   ├── css
│   │   │   └── js
│   │   ├── js
│   │   │   ├── dist
│   │   │   └── src
│   │   ├── package.json
│   │   └── scss
│   │       ├── _alert.scss
│   │       ├── _badge.scss
│   │       ├── ...
│   │       ├── _variables.scss
│   │       ├── bootstrap-grid.scss
│   │       ├── bootstrap-reboot.scss
│   │       ├── bootstrap-utilities.scss
│   │       ├── bootstrap.scss
│   │       ├── forms
│   │       ├── helpers
│   │       ├── mixins
│   │       ├── utilities
│   │       └── vendor
```

L'information sur les dépendences installées vient d'être ajoutée dans le fichier `package.json`. Maintenant votre projet **sait** de quoi il a besoin. Si vous supprimez le dossier `node_modules`, il suffit de taper dans le terminal

```bash
npm install
```

et tout ce dont votre projet a besoin, sera installé.

---

## Step 2

Configurer Sass Live Compiler

- créer un dossier `.vscode` (dans la racine du projet `alyra-challenge-custom-b5` )
- dedans créer un fichier `settings.json`
- reprendre l'exemple de config depuis [la FAQ de plugin Live Sass Compiler](https://ritwickdey.github.io/vscode-live-sass-compiler/docs/faqs.html)
- rien à ajouter, `node_modules` où se trouvent fichiers scss de bootstrap sont déjà exclus

```
{
     "liveSassCompile.settings.formats":[
        {
            "format": "expanded",
            "extensionName": ".css",
            "savePath": "/css"
        },
        {
            "extensionName": ".min.css",
            "format": "compressed",
            "savePath": "/dist/css"
        }
    ],
    "liveSassCompile.settings.excludeList": [
       "**/node_modules/**",
       ".vscode/**"
    ],
    "liveSassCompile.settings.generateMap": true,
    "liveSassCompile.settings.autoprefix": [
        "> 1%",
        "last 2 versions"
    ]
}
```

## Step 3

Lancer `Watch Sass` pour vérifier la configuration.

```scss
// custom/mybootstrap.scss
body {
  color: red;
}
```

On devrait appercevoir des nouveaux dossiers et fichiers comme dans l'aborescence ci-dessous

```bash
├── README.md
├── blog-single.html
├── category.html
├── contact.html
├── css
│   ├── mybootstrap.css
│   └── mybootstrap.css.map
├── custom
│   └── mybootstrap.scss
├── dist
│   └── css
│       ├── mybootstrap.min.css
│       └── mybootstrap.min.css.map
├── images
├── node_modules
├── index.html
├── package.json
├── screenshots
└── style.css
```

## Step 4

Dans les fichiers `.html` remplacer le lien vers le css de bootstrap par le lien vers `dist/css/mybootstrap.min.css`

before :

```html
<link
  rel="stylesheet"
  href="https://stackpath.bootstrapcdn.com/bootstrap/5.0.0-alpha1/css/bootstrap.min.css"
  integrity="sha384-r4NyP46KrjDleawBgD5tp8Y7UzmLA05oM1iAEQ17CSuDqnUK2+k9luXQOfXJCJ4I"
  crossorigin="anonymous"
/>
```

after:

```html
<link rel="stylesheet" href="dist/css/mybootstrap.min.css" />
```

## Step 5

Le fichier principal scss de bootstrap est le `bootstrap.scss` dans le dossier `scss`

D'une manière générale, **il n'est pas une bonne pratique de modifier les fichier sources.** On ne touchera pas aux fichiers dans le dossier `scss.`

Au lieu de le modifier, nous allons copier son contenu et le coller dans notre fichier `scss/bootstrap.scss`

Il nous restera à corriger les chemins vers les fichiers partials.

```scss
// custom/mybootstrap.scss
@import "../node_modules/bootstrap/scss/functions";
@import "../node_modules/bootstrap/scss/variables";
@import "../node_modules/bootstrap/scss/mixins";
@import "../node_modules/bootstrap/scss/utilities";
...
```

Astuce: vous pouvez vous servir de la fonctionnalité "Replace" de VSCode Alt+Cmd/Ctrl+F

cherche : @import "  
replace with : @import "../node_modules/bootstrap/scss/

## Step 6

Commentez les partials dont vous vous ne servez pas.

```scss
// custom/mybootstrap.scss
...
// @import "../node_modules/bootstrap/scss/toasts";
// @import "../node_modules/bootstrap/scss/modal";
// @import "../node_modules/bootstrap/scss/tooltip";
// @import "../node_modules/bootstrap/scss/popover";
@import "../node_modules/bootstrap/scss/scss/carousel";
// @import "../node_modules/bootstrap/scss/spinners";
...

```

## Variables

Ouvrer [SassMeister](https://www.sassmeister.com/)

** Quelle couleur prendra body ? **

Exemple 1 :

```scss
$color: orange;
$color: red;

body {
  background: $color;
}
```

Exemple 2 :

```scss
$color: orange;
$color: red !default;

body {
  background: $color;
}
```

Exemple 2 :

```scss
$color: orange;
$color: red !default;
$color: tomato;

body {
  background: $color;
}
```

## Step 7

En haut du fichier `mybootstrap.scss` ajouter

```scss
$secondary: indigo;
$dark: black;
$light: lavender;
$danger: hotpink;
$box-shadow: 0 2px 10px lavender;
```
