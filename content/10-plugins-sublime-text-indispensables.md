---
title: "10 plugins Sublime Text indispensables"
date: "2016-10-18"
tags:
  - "applications"
coverImage: "10-plugins-sublime-text.jpg"
---

Le monde se divise en deux catégories: ceux qui utilisent Sublime Text, et les autres. Bon, j’exagère un peu, mais si vous êtes comme moi un fervent adepte… que dis-je, un fanatique de Sublime Text, vous avez déjà sûrement croisé la route de gens qui se moquent ouvertement de Sublime Text, parce que ce n’est pas un vrai [IDE](http://fr.wikipedia.org/wiki/Environnement_de_d%C3%A9veloppement), que c’est juste un éditeur de texte, en un peu mieux.

Et bien, à ces gens là, qui vont prêcher du Eclipse, NetBeans ou encore PhpStorm (ce dernier commence d’ailleurs à devenir vraiment très populaire), je répondrai: vous avez tort (ou raison) à 50%.<!--more-->

Certes, à l’origine, Sublime Text est “juste un éditeur de texte”, mais il dispose d’une très grande force: son système de plugins. Et c’est justement via ces plugins qu’il peut se transformer en un outil très, très puissant, pour moi à la hauteur (voire mieux) que les IDE classiques.

Encore faut-il s’y retrouver parmi les centaines - peut être même milliers - de plugins existants. Voici donc sans plus tarder, la liste des plugins que j’utilise et que je recommande fortement à tout développeur (frontend ou backend) qui souhaite disposer d’un outil à la fois puissant, rapide,polyvalent et efficace (rien que ça !).

## [](#1-alignment)1\. Alignment

Ouh qu’il est bon celui-là. Non sérieusement, une fois que vous y avez gouté, c’est dur de s’en passer. Comme son nom l’indique, [Alignment](https://packagecontrol.io/packages/Alignment) va vous permettre d’aligner vos morceaux de codes en une seule combinaison de touches. C’est surtout pratique quand on code pour des langages backend, mais on peut s’en servir partout, même dans de simples fichiers texte.

## [](#2-bracket-highlighter)2\. Bracket Highlighter

Un plugin super simple mais efficace, au nom tout aussi explicite, [Bracket Highlighter](https://github.com/facelessuser/BracketHighlighter) va mettre en surbrillance les parenthèses, crochets et accolades dans votre code.

Ça à l’air bête comme ça mais c’est vraiment pratique. Dès que votre code s’allonge et que vous multipliez les boucles, fonctions et autres, ça permet de s’y retrouver plus facilement.

## [](#3-convert-case)3\. Convert Case

[Convert Case](https://packagecontrol.io/packages/Case%20Conversion) est un plugin qui, comme vous l’aurez deviné, permet de générer des images GIF aléatoires. Non, je plaisante, il fallait que je trouve un truc à dire autre que “encore un plugin au nom explicite”.

Quand on code, on est toujours à alterner entre formatage de texte, que ce soit passer un mot tout en majuscule (ou l’inverse), mais aussi convertir un mot, une expression ou une variable (surtout une variable) en _camelCase_, _underscore case_ (appelé _snake case_) ou encore remplacer les espaces par des tirets.

Ce plugin va vous permettre de convertir vos chaines de caractère entre tous ces formats, en un clin d’oeil. Exemple:

## [](#4-docblockr)4\. DocBlockr

[DockBlockr](https://packagecontrol.io/packages/DocBlockr) s’adresse principalement aux développeurs backend. Ce plugin permet de créer très simplement des [DocBlock](http://en.wikipedia.org/wiki/PHPDoc#DocBlock) pour vos variables, classes et fonctions. Plus besoin de retenir la syntaxe exacte ds commentaires, ou d’aller chercher un exemple sur internet pour faire un copier-coller.

## [](#5-emmet)5\. Emmet

Il est probable que vous l’utilisiez déjà, si vous travaillez avec Sublime Text, mais si ce n’est pas le cas, je vous conseille plus que vivement d’installer le plugin [Emmet](https://github.com/sergeche/emmet-sublime).

Tout simplement indispensable pour tout développeur web (front ou back), dès qu’il s’agit de HTML ou de CSS, Emmet vous fera gagner énormément de temps en transformant vos abréviations en code complet. Par exemple, il vous suffit de taper `html:5` et d’appuyer sur `TAB` pour que cela se transforme en squelette HTML 5 complet. Des heures… des jours de gagnés je vous dis !

## [](#6-gotodocumentation)6\. GotoDocumentation

Rassurez-moi, vous êtes comme moi, vous ne vous souvenez pas de toutes les syntaxes des milliers de fonctions et spécificités de PHP, JS, Python ou C++ ? Et du coup vous faites un petit tour sur la navigateur à chaque fois pour aller chercher la doc qui va bien ? Oui et bien, comme le diraient certains acteurs de publicité presbytes ou myopes, ça, c’était avant !

Il existe un merveilleux petit plugin répondant au doux nom de [SublimeText 2 GotoDocumentation](https://github.com/kemayo/sublime-text-2-goto-documentation) et contrairement à ce que l’on pourrai croire il est parfaitement compatible avec la version 3 de votre éditeur de code préféré. Ce superbe petit plugin donc, va vous permettre de placer votre curseur sur n’importe quelle fonction ou mot-clé d’un langage supporté, et vous serez automatiquement amené vers la page précise de la documentation concernant ce mot-clé.

Les langages supportés sont:

- PHP
- JS / CoffeeScript
- HTML
- CSS/SASS/LESS
- Python (via pydoc)
- Clojure
- Go
- Ruby (+Rails)
- C / C++
- Perl
- C#
- Lua
- Postgres
- Erlang
- Smarty
- Haskell
- ..et vous pouvez rajouter n’importe quel autre langage via les paramètres de configuration.

## [](#7-markdown-editing-markdown-preview)7\. Markdown Editing & Markdown Preview

Allez, je suis comme ça, je vous file deux plugins pour le prix d’un !

J’utilise énormément le [Markdown](http://fr.wikipedia.org/wiki/Markdown), j’adore cette syntaxe (à un tel point que j’écris mes articles de blog en Markdown). Du coup, deux très bon plugins existent pour Sublime Text. Je vous les mets ensemble car, si on peut tout à fait les installer indépendamment, je trouve qu’ils se complètent et fonctionnement à merveille ensemble.

[Markdown Editing](https://packagecontrol.io/packages/MarkdownEditing), dans un premier temps, vous permet d’améliorer considérablement votre expérience lorsque vous rédigez des documents en Markdown, en vous apportant une coloration syntaxique dédiée à ce langage, ainsi qu’un rendu visuel immédiat.

Dans un second temps, [Markdown Preview](https://packagecontrol.io/packages/Markdown%20Preview) va vous permettre rapidement exporter votre contenu Markdown au choix vers un fichier HTML, ou copier le code HTML généré dans votre presse-papier. En plus de cela, vous pourrez choisir entre le parser Python par défaut ou celui de GitHub (pour profiter de la syntaxe [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/)).

Avec ça, on bouffe du Markdown au petit déj’ !

## [](#8-sidebar-enhancements)8\. Sidebar Enhancements

Derrière son nom un peu barbare pour les anglophobes (mais si vous êtes réfractaires à l’anglais et avez choisi de faire du développement web, vous êtes un peu maso), [Sidebar Enhancements](https://packagecontrol.io/packages/SideBarEnhancements) va rendre le menu contextuel du panneau latéral des fichiers beaucoup, beaucoup plus sympa, en vous proposant de nombreuses fonctionnalités bien pratiques.

On s’y fait très vite et les fonctionnalitées ajoutées sont vraiment sympas:

- Ouvrir le fichier courant dans l’explorateur
- Déployer l’arborscence dans Sublime Text jusqu’au fichier (si celui-ci est enterré sous 10 niveaux de dossiers)
- Lancer la recherche & remplacement sur le dossier sélectionné
- Copier rapidement le chemin entier, relatif, absolu ou juste le nom du fichier sélectionné
- Dupliquer, déplacer, renommer un fichier ou un dossier
- Gérer le projet (ajouter un dossier, en exclure, modifier les paramètres du projet)

Et j’en passe.

## [](#9-sublime-github)9\. Sublime-GitHub

À ne pas confondre avec GitHub Tools, [Sublime GitHub](https://packagecontrol.io/packages/sublime-github) va vous être très pratique si vous utilisez [Gist](https://gist.github.com/), une application de GitHub qui vous permet de stocker tous vos “snippets” ou morceaux de codes.

Vous pourrez créer, sauvegarder et rapatrier tous vos gists depuis Sublime Text.

Si vous avez le plugin Git également d’installé, vous disposerez de fonctions supplémentaires pour analyer vos fichiers sur GitHub.

Le petit truc sympa en plus, c’est que ce plugin peut fonctionner avec plusieurs comptes GitHub à la fois.

## [](#10-tag)10\. Tag

[Tag](https://github.com/titoBouzout/Tag), c’est un peu la visseuse automatique du HTML. On peut faire sans mais c’est quand même vachement plus pratique et rapide avec. Si vous travaillez souvent avec du HTML, Tag vous faire gagner énormément de temps en vous permettant de rapidement:

- de fermer automatiquement vos balises HTML
- d’auto-indenter/formater votre code HTML/XML
- de supprimer rapidement des balises HTML autour d’un bloc de texte ou de votre sélection
- de supprimer automatiquement les attributs d’une balise
- de détecter vos balises mal fermées

Et voilà ma liste de plugins préférés, ceux que j’utilise énormément au quotidient et dont je ne peux plus me passer ! Si vous connaissez des plugins bien sympas qui ne sont pas listés ici, n’hésitez pas à me les partager dans les commentaires.
