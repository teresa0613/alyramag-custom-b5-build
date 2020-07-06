# Alyra Bootstrap Challenge - Custom Bootstrap5 CSS build

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

DCopier le dossier scss depuis les fichiers source de [Bootstrap 5](https://www.dropbox.com/s/q3hj2vzhkm6kkwl/Screenshot%202020-06-30%2012.46.45.png?dl=0) et coller-le dans la racine du projet `alyra-challenge-custom-b5`

![](https://wptemplates.pehaa.com/assets/alyra/b5source.png)

---

## Step 2

Configurer Sass Live Compiler

- créer un dossier `.vscode` (dans la racine du projet `alyra-challenge-custom-b5` )
- dedans créer un fichier `settings.json`
- reprendre l'exemple de config depuis [la FAQ de plugin Live Sass Compiler](https://ritwickdey.github.io/vscode-live-sass-compiler/docs/faqs.html)
- ajouter `"scss/**"` dans `"liveSassCompile.settings.excludeList"` (comme ci-dessus)

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

D'une manière générale, **il n'est pas une bonne pratique de modifier les fichier sources.** On ne touchera pas aux fichiers dans le dossier `scss.`

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
