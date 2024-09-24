---
title: "Afficher un widget WordPress uniquement sur certaines pages"
date: "2016-09-13"
tags:
  - "code"
coverImage: "wordpress-afficher-widget-selon-la-page.jpg"
---

Ah, un petit tutoriel sur WordPress, ça faisait longtemps !

Les widgets de WordPress sont un des éléments qui ont fait le succès du [CMS](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_contenu) le plus populaire au monde.

Ce système de modules, très pratique, permet de placer des blocs proposant du contenu (texte, HTML, images...) ou des fonctionnalités (formulaires, fil d'actualité Twitter, Facebook like box) n'importe où facilement à l'aide de glisser-déposer.

Pourtant, le comportement par défaut fait que, lorsque par exemple vous placez un widget dans votre sidebar, celui-ci apparaîtra automatiquement sur l'ensemble de votre blog.

Mais si jamais vous souhaitez afficher un widget uniquement sur une page en particulier, comment faire ? Je vais vous donner 3 méthodes pour y parvenir.<!--more-->

## Créer et Utiliser Une Sidebar Différente

Si vous connaissez un peu le principe des thèmes WordPress, vous devez savoir que par défaut, il faut au moins un fichier `sidebar.php` pour contenir les widgets. Ce fichier contient la fonction `get_sidebar()` pour afficher les widgets.

Une solution simple est alors de créer plusieurs fichiers de sidebar afin de pouvoir choisir, dans le panneau d'administration de WordPress, dans laquelle placer nos widgets.

Par exemple, admettons que vous ayez une page **Contact**, dans laquelle vous voudriez avoir une sidebar différente des autres pages. Vous pouvez alors créer un nouveau fichier de sidebar, en l'appelant par exemple `sidebar-contact.php`.

Ensuite, si ce n'est pas déjà le cas, créez également un template pour la page contact (`contact.php`. Vous devez utiliser l'identifiant de la page comme nom de fichier). À l'intérieur, là où vous voulez placer votre sidebar, insérez le code suivant: `get_sidebar('contact');` Ainsi, tous les widgets que vous placerez dans la sidebar "Contact" apparaîtront uniquement sur la page de contact.

## Utiliser les Tags Conditionnels

L'inconvénient de la première méthode, c'est qu'il faut créer au préalable un template personnalisé pour les pages dont vous souhaitez personnaliser la sidebar.

Une solution qui ne nécessite pas de créer de template consiste à utiliser les **tags conditionnels**.

En reprenant le même exemple, pour personnaliser la page de contact, il vous suffit modifier le fichier `page.php`, qui est le template par défaut de toutes les pages, et d'y ajouter ce code: `if ( is_page('contact') ) {   get_sidebar( 'contact' );   } else {   get_sidebar();   }` Ce code va vous permettre de n'afficher la sidebar "Contact" que sur la page de contact. Vous pouvez ainsi étendre le jeu de conditions pour afficher des sidebars supplémentaires en fonction d'autres pages.

## Avec JetPack

Si vous ne connaissez pas **JetPack**, je vous conseille d'y [jeter un coup d'oeil](http://wordpress.org/plugins/jetpack/). Il s'agit d'une extension qui, en réalité, regroupe plusieurs plugins très pratique (qu'on retrouve lorsqu'on utilise [Wordpress.com](http://wordpress.com)).

Dans **JetPack**, activez le module **Widget Visibility**.

![](images/wordpress-widget-visiblity.jpg)

Puis, dans la page des widgets du panneau d’administration, vous devriez voir apparaître une nouvelle option dans les widgets, intitulé "Visibilité", qui va vous permettre de choisir sur quelle page afficher ou masquer un widget.

![](images/wordpress-widget-visibility-2.jpg)

Notez que cette dernière méthode est intéressante pour deux raisons: premièrement, vous n'avez pas à toucher à vos fichiers PHP et deuxièmement, vous pourrez même choisir sur quel _type de page_ afficher un widget (par exemple, sur la page d'erreur 404, sur les résultats de recherche, etc...).

J'espère que ces astuces vous seront utiles. Si vous avez des questions ou des doutes à ce sujet, n'hésitez surtout pas à poser des questions dans les commentaires.

Source: [Hongkiat](http://www.hongkiat.com/blog/wordpress-conditional-widget/)
