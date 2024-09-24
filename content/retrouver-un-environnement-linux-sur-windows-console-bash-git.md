---
title: "Retrouver un environnement Linux sur Windows (console bash, GIT)"
date: "2016-02-09"
tags:
  - "code"
coverImage: "shell.jpg"
---

Lorsque je développe, la plupart du temps je dois me servir du [shell Unix](http://fr.wikipedia.org/wiki/Shell_Unix "Qu'est ce que le shell Unix"). Pour certains projets ce n'est pas nécessaire, mais pour d'autres, c'est plus pratique (surtout quand on utilise Symfony), voire indispensable.<!--more-->

Hors pour se servir d'une console unix, eh bien il faut un système Unix, genre Linux. Donc si vous bossez sur Linux, pas de soucis. Mais si vous êtes sur Windows, c'est une autre paire de manche. Il faut avoir un serveur dédié (ou au moins un VPS), sinon il faut bricoler (comme utiliser une machine virtuelle).

Jusqu'ici j'avais un serveur dédié à la maison, car pour mon ordinateur personnel, je suis sous Windows. J'y ai mes habitudes et mes réflexes, j'avoue être satisfait de mon OS. Donc même si j'aime bien Linux et que c'est le top pour faire du dev, je ne souhaite pas changer de système.

Malgré tout, je me suis quand même posé la question: **est ce qu'il serait possible de se passer d'un serveur domestique ou dédié ("lourd" à gérer) pour bénéficier des avantages de la console unix sous Windows ? La réponse est oui**.

## Plusieurs solutions, et la meilleure selon moi...

Tout d'abord, vous pouvez essayer de vous dépatouiller avec la console basique de Windows, "**cmd.exe**". Mais bon, bonjour la galère ! A éviter, surtout si vous avez l'habitude des commandes Linux.

L'alternative la plus connue est [Cygwin](http://fr.wikipedia.org/wiki/Cygwin "Qu'est ce que Cygwin"). Pour faire simple, il s'agit d'une suite d'outils qui vont permettre de simuler un environnement Linux dans windows, afin de pouvoir utiliser des commandes Unix dans la console basique Windows. Sympa, mais assez lourd à installer et mettre en place. La solution que j'avais alors installé, sans vraiment l'utiliser, était [GOW](https://github.com/bmatzelle/gow "Aller sur le site de GOW") (Gnu On Windows). Un peu le même principe que Cygwin, c'est à dire ajouter à la console de base Windows plus de 130 commandes du shell Unix (ls, mv, rm, touch, etc...), mais en plus léger. Malgré tout, ce n'était pas encore vraiment la panacée.

### Enfin une "vraie" console Linux

Après une courte recherche, aujourd'hui j'ai découvert [**msysGit**](https://git-for-windows.github.io/ "Aller sur le site de msysGit"). Il s'agit d'un package "tout-en-un" qu'il suffit d'installer et qui va vous permettre de disposer à la fois d'une **console type bash linux très pratique, et en plus vous aurez GIT** à la dernière version (ou presque) installé et fonctionnel, prêt à être utilisé ! Que demander de plus ? Une console plus jolie que celle par défaut dans Windows, et qui ressemble encore plus à un terminal Linux :)

### Customisation

J'aurai pu simplement m'arrêter là, mais je ne trouvais pas l'interface assez ressemblante à un vrai terminal Linux. Je l'ai donc améliorée en implémentant ce bash avec [Console2](http://sourceforge.net/projects/console/ "Voir le site de Console2"). En gros, Console2, ce n'est pas comme son nom pourrait le laisser penser une console, mais plutôt un logiciel qui va améliorer l'interface de votre console. Et vous pouvez donc choisir quelle console utiliser avec: soit la console de windows, soit le bash de msysGit (c'est celui ci que nous allons utiliser).

## Installation et configuration en détails

Bon, tout ça c'est bien beau, maintenant, passons au choses sérieuses, et voyons comment faire pour obtenir une belle console Unix dans notre Windows. Cela se déroule en  4 étapes :

1. Installation de msysGIT
2. Installation et configuration de Console 2
3. Configuration de l'environnement de travail (alias, PATH, homedir)
4. Bonus: configurer un éditeur de texte

### 1.Installation de msysGIT

Rien de compliqué. Allez sur la page de [téléchargement de msysGIT](http://code.google.com/p/msysgit/downloads/list?can=2&q=&colspec=Filename+Summary+Uploaded+ReleaseDate+Size+DownloadCount) et choisissez la version à installer. Personnellement, j'ai pris [la version la plus récente de GIT et portable](http://code.google.com/p/msysgit/downloads/detail?name=PortableGit-1.8.0-preview20121022.7z&can=2&q= "Version portable de msysGIT"), car je ne jure que par les versions portables, bien plus pratique à mon goût. D'ailleurs avec cette version, il n'y a rien d'autre à faire que de décompresser l'archive 7-zip dans le dossier de votre choix, et c'est bon ! Tout est fonctionnel directement (vous pouvez essayer l'application en lançant "**git-bash.cmd**".

### 2.Installation et configuration de Console 2

[Téléchargez Console2](http://sourceforge.net/projects/console/files/latest/download) et décompressez l'archive dans le dossier de votre choix. Personnellement, j'ai choisi de l'installer dans le même dossier que **msysGIT**, cela me parait le plus logique. Console2 est également portable (c'est pas beau ça ?), ce qui veut dire que vous n'avez rien d'autre à faire une fois l'archive extraite.

Pour tester le logiciel, lancer "**Console.exe**". **Configuration**: en lançant la première fois Console2, vous devriez vous apercevoir que celle-ci utilise par défaut la console Windows de base. Ce n'est pas ce que nous voulons. Configurons donc Console2 pour fonctionner avec le bash de msysGIT. Pour ce faire, une fois Console2 lancé, allez dans **Edit > Settings**, et le premier menu de gauche, **Console**. A droite, vous verrez que dans la première ligne vous pouvez choisir le shell à utiliser. Choisissez le fichier **bash.exe** situé dans le dossier **bin** du répertoire où vous avez extrait msysGit. Par exemple, pour moi, le chemin est: `D:\msysgit\bin\bash.exe`. Ajoutez à la fin de la ligne (séparé par un espace)  `--login -i`. Pour mon exemple, cela donne au final: `D:\msysgit\bin\bash.exe --login -i` 

Fermez et redémarrez la console, elle devrait maintenant utiliser la bash de msysGIT. Vous pouvez également changer les touches de raccourci et les actions au clic dans **Edit > Settings > Hotkeys**. Par exemple, j'ai mis la sélection au clic de souris gauche.

### 3.Configuration de l'environnement de travail (alias, PATH, homedir)

Pour que notre environnement ressemble vraiment à un terminal Linux, il faut procéder à plusieurs configurations.

- **Répertoire utilisateur et path pour PHP**: premièrement, on va définir les paramètres par défaut. En ouvrant la console, le répertoire racine "/" est le dossier d'installation de msysGIT. Nous allons donc créer le fichier **/etc/bash\_profile** qui sera exécuté à chaque démarrage de la console. Dedans, copiez-y ce texte:

    ```
    HOME="/home/nomdutilisateur"
    export PATH=$PATH:/D/xampp/php
    ```

    La première ligne va définir notre dossier utilisateur par défaut. Vous devinez donc qu'il faut créer le dossier correspondant: **/home/votrenomdutilisateur**. La deuxième ligne elle va renseigner le chemin de PHP, pour que vous puissiez utiliser PHP en mode CLI directement dans la console. Remplacez le chemin par le bon (le votre) chemin d'installation de PHP._**EDIT: il semble qu'il n'est pas obligatoire de preciser la lettre de lecteur / partition dans le PATH. Ex:**_

    ```
    export PATH=$PATH:/xampp/php:/ruby/bin
    ```

- **Paramètres utilisateurs**: pas obligatoire mais très pratique, créez le fichier **/home/nomdutilisateur/.bash\_profile** pour y mettre le contenu suivant:

    ```
    # Custom prompt
    PS1='\[\e[32;1m\]\u\[\e[31;1m\]@\H\[\e[34;1m\]:\w\[\e[37;1m\] $ \[\e[0m\]'# Aliases
    alias ll='ls -laF --color --show-control-chars'
    ```

    La première instruction est pour personnaliser l'invite de commande (qui affichera `votrenomdutilisateur@nomdevotremachine:répertoire $`). La deuxième, c'est un alias perso, vous pouvez y mettre tous vos alias.

Encore une fois, fermez et relancer la console pour que les changements soient pris en compte. Il reste une dernière modification à faire (optionnelle): en fait, quand vous lancez Console2, la console démarre dans le dossier de l'application. Vous pouvez changer l'emplacement par défaut à l'arrivée de l'invite de commande. Pour cela il faut simplement éditer votre raccourci, en modifier le champ "Emplacement" ou "Démarrer dans", qui est vide par défaut, et y mettre le chemin dans lequel vous voulez atterrir par défaut.

**Mise à jour: il semblerai que cette méthode ne fonctionne pas (ça n'a pas marché chez moi en tout cas). Pour pallier à cela, vous pouvez simplement rajouter cette commande dans votre fichier** `/home/nomdutilisateur/.bash_profile`:

```
cd ~
```

Votre fichier .bash\_profile étant appelé à chaque lancement de console, vous atterrirez systématiquement dans votre dossier HOME.

Voilà, votre console est configurée et prête à l'emploi. Vous pourrez utiliser GIT et PHP immédiatement.

### 4.Bonus: configurer un éditeur de texte

Prenons N**otepadMod2**. Mon exécutable se trouve dans: **D:\\Apps\\Notepad2-modPortable**. Dans le dossier /bin/ de msysGIT, créez un fichier nommé, par exemple, "**npad**" (sans extension). A l'intérieur de ce fichier, copiez-le texte suivant:

```
 #!/bin/sh "D:\Apps\Notepad2-modPortable\Notepad2-modPortable.exe" "$*"
```

Bien évidemment, le chemin est à remplacer par celui de l'exécutable que vous souhaitez. Enregistrez le fichier, et c'est tout. Il vous suffit dorénavant, dans la console, de taper `npad fichier.php` et vous pourrez éditer le fichier voulu dans votre éditeur favori. Avec tout ça, normalement, vous devriez vous sentir un peu comme sous Linux dans Windows :)

Sources: [http://buildstarted.com/2012/05/11/replacing-default-git-bash-console-with-console2/](http://buildstarted.com/2012/05/11/replacing-default-git-bash-console-with-console2/) [http://danlimerick.wordpress.com/2011/06/10/git-for-windows-tip-setting-shell-aliases-with-msysgit/](http://danlimerick.wordpress.com/2011/06/10/git-for-windows-tip-setting-shell-aliases-with-msysgit/) [http://danlimerick.wordpress.com/2011/07/11/git-for-windows-tip-setting-home-and-the-startup-directory/ http://danlimerick.wordpress.com/2011/06/12/git-for-windows-tip-setting-an-editor/](http://danlimerick.wordpress.com/2011/07/11/git-for-windows-tip-setting-home-and-the-startup-directory/) [http://mohundro.com/blog/2010/02/04/some-tips-on-using-git-with-windows/](http://mohundro.com/blog/2010/02/04/some-tips-on-using-git-with-windows/) [http://markashleybell.com/articles/portable-git-windows-setting-home-environment-variable](http://markashleybell.com/articles/portable-git-windows-setting-home-environment-variable) [http://superuser.com/questions/132711/how-to-copy-text-from-console2](http://superuser.com/questions/132711/how-to-copy-text-from-console2) [http://gregk.me/2011/change-gitbash-home-directory/](http://gregk.me/2011/change-gitbash-home-directory/) [](http://mohundro.com/blog/2010/02/04/some-tips-on-using-git-with-windows/)
