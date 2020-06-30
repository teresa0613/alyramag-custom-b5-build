# Alyra Bootstrap Challenge - Custom Bootstrap5 build (sass -> css)

[demo](https://alyra-bootstrap-chlng.netlify.app/)

## Step 0

Créer un dossier custom

```bash
mkdir custom
```

Ajouter un fichier

```bash
touch custom/mybootstrap.scss
```

## Step 1

Copier le dossier scss depuis les fichier source de Bootstrap 5

## Step 2

Configurer Sass Live Compiler

- créer un dossier `.vscode`
- créer un fichier `settings.json`

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
       ".vscode/**",
       "scss/**"
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
├── index.html
├── screenshots
├── scss
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

Il n'est pas une bonne pratique de modifier les fichier sources. C'est un règle générale.

Au lieu de le modifier, nous allons copier son contenu et le coller dans notre fichier `scss/bootstrap.scss`

Il nous restera à corriger les chemins vers les fichiers partials.

```scss
// custom/mybootstrap.scss
@import "../scss/functions";
@import "../scss/variables";
@import "../scss/mixins";
@import "../scss/utilities";
...
```

Astuce: vous pouvez vous servir de la fonctionnalité "Replace" de VSCode Alt+Cmd/Ctrl+F

cherche : @import "  
replace with : @import "../scss/

![](https://wptemplates.pehaa.com/assets/alyra/replace.png)

## Step 6

Commentez les partials dont vous vous ne servez pas.

```scss
// custom/mybootstrap.scss
...
// @import "../scss/toasts";
// @import "../scss/modal";
// @import "../scss/tooltip";
// @import "../scss/popover";
@import "../scss/carousel";
// @import "../scss/spinners";
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
$colot: tomato;

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
