---
title: "Résoudre les problèmes de javascript dans l'admin WordPress"
date: "2016-05-10"
tags:
  - "code"
coverImage: "wordpress-nginx-javascript.jpg"
---

Il vient de m'arriver un truc bizarre avec l'un de mes sites tournant sous [WordPress](http://wordpress-fr.org). Si vous êtes utilisateur de Wordpress (du moins la version qu'on héberge soi-même), ce genre de souci peut vous arriver.<!--more-->

Je voulais tranquillement éditer un article lorsque je me suis aperçu que l'éditeur [WYSIWIG](http://fr.wikipedia.org/wiki/What_you_see_is_what_you_get) n'apparaissait pas. Pire plus aucune fonction faisant appel au Javascript ne voulait fonctionner (insertion d'image, changement d'onglet). Encore plus bizarre, parfois lorsque j'actualisais la page, tout se remettait à fonctionner, puis au chargement suivant, re-belote, plus rien qui marche.

Réflexe de développeur, j'ouvre la console, et je m'aperçois qu'il y a tout plein d'erreurs Javascript. Là où je me suis pris la tête, c'est que j'ai strictement la même version du site en local sur mon ordinateur, et je ne rencontre pas du tout le même souci. Ce dont je me suis aperçu, c'est que, pour la version sur mon serveur, les fichiers javascripts chargés par l'interface d'administration étaient coupés en plein milieu !

Il y a très peu de ressources sur le net qui abordent ce souci, qui n'est pas si commun, alors je vous donne la solution qui a fonctionné pour moi. En réalité le "souci" venait de [NGINX](http://fr.wikipedia.org/wiki/Nginx). NGINX a par défaut une sorte de limite de rendu pour la taille des fichiers statiques, comme les fichiers **CSS** ou **javascript**. Et lorsqu'un fichier est très long, comme c'est le cas pour certains javascripts utilisés par Wordpress (qui en réalité compacte plusieurs fichiers en un seul), celui-ci peut se retrouver "coupé" en plein milieux, et donc causer une erreur javascript qui du coup fait planter tout le reste.

**La solution consiste donc à paramétrer NGINX** (dans votre fichier de vhost ou directement dans le fichier de configuration globale `nginx.conf`, à vous de voir) pour lui dire d'augmenter la limite de taille pour servir les fichiers statiques. Pour ce faire, ajouter dans votre fichier de configuration le paramètre suivant:

```
fastcgi_buffers 128 4k;
```

Si cela ne suffit pas vous pouvez remplacer `128` par `256`.
