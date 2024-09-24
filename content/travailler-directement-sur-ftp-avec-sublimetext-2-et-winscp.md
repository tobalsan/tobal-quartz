---
title: "Travailler Directement sur FTP avec Sublime Text et WinSCP"
date: "2016-03-15"
tags:
  - "astuces"
coverImage: "sublime-winscp.jpg"
---

Enfin ! Je suis un grand fan de SublimeText, mais mon plus gros grief pendant longtemps était de ne pas pouvoir travailler directement sur un serveur FTP. D'ailleurs je sais que certaines personnes restent sous Notepad++ car elle travaillent beaucoup directement sur FTP, et le plugin intégré à Notepad++ fait bien son boulot.

Mais j'ai une bonne nouvelle pour ces personnes là: il y une méthode pour profiter de SublimeText tout en travaillant directement sur FTP.<!--more-->

En général je travaille en local, mais souvent j'ai besoin d'éditer des fichier rapidement sur un serveur pour une petite modification. Il y a bien un [plugin](http://wbond.net/sublime_packages/sftp), mais premièrement, il est payant, et deuxièmement, je ne le trouve pas forcément ergonomique. Il synchronise d'abord un dossier en local, puis on édite les fichiers en local pour les synchroniser avec le serveur.

Mais j'ai récemment trouvé un alternative très pratique: [WinSCP](http://winscp.net/eng/docs/lang:fr). En le couplant avec SublimeText, il devient alors très facile et rapide de modifier et créer des fichiers (et dossiers) directement sur un serveur FTP. Voici comment faire.

Ce mini tuto est dispo [en vidéo](#video "Voir la vidéo").

## [](#configurer-winscp)Configurer WinSCP

Commencez par lancer WinSCP (vous pouvez le [télécharger ici](http://winscp.net/eng/download.php). Personnellement, j'utilise la [version portable](http://portableapps.com/apps/internet/winscp_portable)).

Vous devriez avoir ceci: [![](https://github-camo.global.ssl.fastly.net/8f30a112474e77edc24a17be79b996302f35a74f/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702e706e67)](https://github-camo.global.ssl.fastly.net/8f30a112474e77edc24a17be79b996302f35a74f/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702e706e67)

 

Cliquez sur le menu**Préférences** puis sélectionnez l'affichage **Explorer**.

[![](https://github-camo.global.ssl.fastly.net/6b873c27a6df9279ff73bc4b0b1a11b031cf37ef/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d70726566732e706e67)](https://github-camo.global.ssl.fastly.net/6b873c27a6df9279ff73bc4b0b1a11b031cf37ef/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d70726566732e706e67)

 

Ce type d'affichage permet de n'afficher que les fichiers sur le serveur FTP distant (au contraire du mode **Commander** qui, à la manière de FileZilla, vous affichera aussi une fenêtre de vos fichiers locaux).

Toujours dans la même fenêtre, cliquez sur le bouton **Préférences**, afin d'ouvrir les préférences avancées. Puis cliquez sur **Éditeurs**. Il s'agit de la liste des éditeurs associés pour ouvrir des fichiers quand vous double-cliquez dessus dans WinSCP.

[![](https://github-camo.global.ssl.fastly.net/d759943b55607833e4fb761cadd5e35407db8255/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d65646974657572732e706e67)](https://github-camo.global.ssl.fastly.net/d759943b55607833e4fb761cadd5e35407db8255/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d65646974657572732e706e67)

 

Vous allez donc ajouter SublimeText. Cliquez sur **Ajouter** et renseignez le chemin vers l'exécutable de SublimeText (par exemple _C:\\Program Files\\SublimeText\\sublime\_text.exe_). Décochez également la case correspondant à _Forcer transfert en mode texte..._ (la deuxième):

[![](https://github-camo.global.ssl.fastly.net/05ae4a67d2ecaf797d5fdc266be82e2253cca9de/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d656469746575722d64657461696c732e706e67)](https://github-camo.global.ssl.fastly.net/05ae4a67d2ecaf797d5fdc266be82e2253cca9de/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d656469746575722d64657461696c732e706e67)

 

Quand vous validez, SublimeText devrait apparaître en deuxième ligne. Cliquez sur **Monter** afin de le mettre en première position, pour que ce soit l'éditeur par défaut pour tous les fichiers.

Validez, puis connectez-vous (créez une nouvelle session si besoin). Vous verrez alors une fenêtre à deux espaces: celui de gauche présente l'arborescence des dossiers du serveur et celui de droite les fichiers du dossier courant.

[![](https://github-camo.global.ssl.fastly.net/8636787faf83813961e16d63f80313a9210a8620/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d696e746572666163652e706e67)](https://github-camo.global.ssl.fastly.net/8636787faf83813961e16d63f80313a9210a8620/687474703a2f2f737277656273697465732e73332e616d617a6f6e6177732e636f6d2f736d617274726f636b2f706f7374696d672f77696e7363702d696e746572666163652e706e67)

 

Il vous suffit alors de double cliquer sur n'importe quel fichier, et il s'ouvrira automatiquement dans SublimeText. Éditez-le, puis enregistrez-le, toujours dans SublimeText, et WinSCP mettra immédiatement à jour le fichier sur le serveur FTP.

Vous pouvez aussi créer, renommer et supprimer des fichiers et dossiers en utilisant le menu contextuel de WinSCP.

Si vous étiez réticents à passer sur SublimeText uniquement pour cette histoire de FTP, voilà qui devrait finir de vous convertir.

### Tuto en vidéo:

<iframe src="//www.youtube.com/embed/D58jes9bjbE" height="474" width="632" allowfullscreen frameborder="0"></iframe>
