---
title: "Renommer le dossier wp-content de WordPress"
date: "2016-06-21"
tags:
  - "code"
coverImage: "renommer-wp-content-wordpress.jpg"
---

Je ne pense pas me tromper en disant que [Wordpress](http://wordpress-fr.org) est devenu, depuis quelques années, un des [CMS](http://fr.wikipedia.org/wiki/Syst%C3%A8me_de_gestion_de_contenu) les plus populaires, si ce n'est LE plus populaire. On recense à travers le monde entier une communauté de près de 80 millions d'utilisateurs de Wordpress. Saviez-vous par exemple que, parmi le million de sites les plus visités au monde, 1 sur 7 utilise Wordpress ? Même ce site fonctionne avec d'ailleurs.

Donc, si vous utilisez Wordpress, vous devez savoir que tous vos thèmes, plugins, images et autres éléments importants de votre site se trouvent dans le dossier **wp-content**.<!--more-->

![](images/dossier-wp-content.jpg)

Mais saviez-vous que vous pouviez renommer ce dossier ? Vous pouvez l'appeler comme bon vous semble, et cela a plusieurs avantages. D'une, cela vous permet de "customiser" encore un peu plus votre site et de le rendre moins "Wordpressisé" (oui j'invente des mots), et d'autre part, cela ajoute un brin de sécurité supplémentaire (vu que les méchant hackers qui connaissent bien Wordpress vont chercher directement le dossier **wp-content**).

Mais si vous essayez juste de renommer le dossier, vous allez vous apercevoir que votre site va très mal fonctionner. Alors comment faire pour ne pas tout casser ? C'est relativement simple mais il faut suivre impérativement les étapes suivantes.

## 1\. Renommez Le Dossier wp-content

Oui, vous allez tout casser, c'est pas grave, faites-le. Renommez votre dossier **wp-content**, en **composants** (exemple pris au pif, mettez le nom qui vous plait, pinocchio ou songoku si ça vous chante).

En fait à ce moment, votre site se "casse" car par défaut, Wordpress est configuré pour aller chercher tout ce qui est important (thèmes, plugins, images, css, etc...) dans un dossier nommé "wp-content". Vous devriez donc voir dans le panneau d'administration des messages d'erreur ce genre:

![](images/rename-wp-content-1.jpg) ![](images/rename-wp-content-2.jpg)

Le message indique que les plugins ont été désactivés à cause d'une erreur: les fichiers de plugins n'existent pas. Normal, on a renommé le dossier wp-content.

## 2\. Mise À Jour Du Fichier De Configuration

Pour résoudre ces soucis, il va falloir que vous mettiez à jour le fichier principal de configuration de Wordpress **wp-config.php**. Faites d'abord une copie du fichier, au cas où, comme ça même si vous faites n'importe quoi vous avez une issue de secours. Ensuite, pour indiquer à Wordpress le bon dossier dans lequel chercher, insérez juste avant la ligne \[cci lang="php"\]require\_once(ABSPATH . 'wp-settings.php') (en général cette ligne est la dernière, tout en bas à la fin du fichier), les lignes suivantes:

\[cc lang="php"\] define ('WP\_CONTENT\_FOLDERNAME', 'composants'); define ('WP\_CONTENT\_DIR', ABSPATH . WP\_CONTENT\_FOLDERNAME) ;

Ceci indiquera à Wordpress d'aller chercher les thèmes et plugins dans le dossier **composants**. Changez "**composants**" dans le code si vous avez opté pour un autre nom, évidemment.

Vos thèmes et plugins devraient être revenus.

![](images/rename-wp-content-3.jpg)

En revanche, vous devrez peut-être les réactiver.

## 3\. Corriger Aussi Les Liens

Vous avez presque fini. Cependant, en laissant les choses comme ça, vous vous apercevrez que les images, par exemple, ne s'affichent plus. C'est parce qu'il y a une autre (et derniere) chose à ajouter dans le code, pour indiquer à Wordpress, lorsqu'il génère les liens vers les images et autres éléments de thème, le bon chemin à afficher. Ajouter donc ces deux lignes dans votre fichier **wp-config.php**, à la suite des précédentes:

\[cc lang="php"\] define('WP\_SITEURL', 'http://' . $\_SERVER\['HTTP\_HOST'\] . '/'); define('WP\_CONTENT\_URL', WP\_SITEURL . WP\_CONTENT\_FOLDERNAME);

Et voilà ! Votre site Wordpress aura pour dossier de thèmes et de plugins le dossier avec le nom que vous aurez choisi.

## Remarques Importantes

Dans la dernière modification, si vous êtes en [https](http://fr.wikipedia.org/wiki/Https), n'oubliez pas de modifier la ligne contenant "http" en conséquence.

Ensuite, il y a forcément des thèmes et des plugins qui ne respectent pas les bonne pratiques de codage, et qui mettent le nom du dossier "wp-content" directement en dur dans le code (au lieu de le générer dynamiquement grâce aux fonctions Wordpress). Dans ce cas-là, ces plugins et thèmes cesseront de fonctionner, tout simplement.

Pour finir, le changement de nom du dossier n'est pas rétroactif: si vous faites cette modification alors que vous avez déjà crée des pages ou des articles, ceux-ci auront l'ancien nom de dossier sauvegardé, et ils ne seront pas mis à jour. Pour pouvoir mettre à jour tout votre contenu sans devenir fou, je vous conseille l'excellent [Wordpress DB Search And Replace](http://interconnectit.com/products/search-and-replace-for-wordpress-databases/). Faites quand même attention quand vous l'utilisez, car c'est un outil automatisé et vous pouvez vite mettre le souk dans votre base de données si vous ne faites pas gaffe (ça tombe bien, il était temps de faire une sauvegarde de votre base de données, non ?).

En général, il vaut mieux effectuer cette manipulation dès le début, au moment où vous installez votre site web.
