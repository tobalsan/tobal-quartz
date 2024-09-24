---
title: "Serveur web Vagrant lent sous Windows (notamment avec Symfony) ? Voici la vraie solution"
date: "2016-10-11"
tags:
  - "code"
coverImage: "vagrant-symfony-serveur-lent.jpg"
---

_Note: ceci est un article technique destiné aux développeurs. Je raconte un peu ma vie au début pour présenter Vagrant. Pour voir directement la solution, sautez les 2 premières parties._

J’ai découvert [Vagrant](http://www.vagrantup.com/) il y a quelques mois, et depuis je ne peu plus m’en passer. Avant, sous Windows, je passais par le célèbre [XAMPP](https://www.apachefriends.org/fr/index.html). Mais ça, c’était avant.<!--more-->

XAMPP est un très bon stack de développement Web, mais le problème bien connu, c’est que votre environnement est complètement différent de celui sur lequel votre site - une fois le développement terminé - finira. La solution apportée par Vagrant est directe et efficace: simplifier la mise en place de machines virtuelles pour permettre aux développeurs de travailler tout de suite dans un environnement identique, ou presque, à un serveur de production.

Il y a vraiment tout un tas d’autres avantages à utiliser Vagrant, mais ce n’est pas le but de ce billet. Je vous encourage à aller [sur le site de Vagrant](http://www.vagrantup.com/) pour en découvrir plus.

## [](#le-souci-un-serveur-web-extremement-lent)Le Souci: Un Serveur Web Extrêmement Lent

Revenons à nos moutons. Je développe énormément à l’aide du framework [Symfony2](http://www.symfony.com) et, lorsque je suis passé à Vagrant, j’ai pu observer un phénomène fort désagréable: le temps de chargement de mes pages était devenu catastrophique:

![Temps de chargement Symfony2 avant](images/2014-07-22_19.03.15.png)

8 secondes pour charger une page sous Symfony2 ! Au premier chargement (quand le cache est vide), le temps de chargement prend entre 8 et 10 secondes. Une fois la mise en cache faite, le temps redescend entre 3 et 5 secondes. Quand on est en train de développer un site, sachant qu’on rafraîchit les pages à peu près 50 fois par heure, c’est horriblement lent.

Pourtant, je ne m’en suis pas tout de suite offusqué. Croyez-le ou non, je me suis simplement dit que c’était plus ou moins normal, que ce devait être dû à l’utilisation de Vagrant (après tout, on utilise une machine virtuelle). Et puis Symfony, en mode `dev`, c’est toujours “un peu plus lent”.

Mais j’ai commencé à me poser des questions lorsque j’ai lancé un script php simple, donc pas de Symfony. Même pour un script qui tient sur une seule page, et qui s’affiche quasi-instantanément en temps normal, prenait quelques secondes quand je passais par mon serveur sous Vagrant. Et puis, je me suis rappelé que je suis sur un disque dur SSD. Il y avait forcément un souci.

## [](#les-solutions)Les Solutions…

Une petite recherche Google m’a confirmé que c’était bien un vrai problème, que plein d’autres avant moi ont rencontré. Pour expliquer cette lenteur de serveur web, les explications les plus courantes rencontrées sont:

- Un problème au niveau du système de fichiers. Sur la machine virtuelle, vous utilisez probablement Linux, et c’est un fait notoire qu’un dossier synchronisé entre Linux et un autre OS (Windows, OSX) provoque des lenteurs, du moins dans le cadre d’une utilisation de machine virtuelle. Donc si votre projet contient plusieurs milliers de fichiers (comme c’est le cas avec Symfony2 et le dossier `vendor`), ça va ramer
- Pour le même souci, le fait que Symfony fasse énormément d’opérations d’écriture pour la compilation du cache pour chaque page, ainsi que l’écriture des logs.
- L’extension XDebug qui fait ramer PHP

C’est sur ce [billet de blog](http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html) que j’ai trouvé le plus d’information sur le sujet.

Si la solution de configurer les dossiers synchronisés pour utiliser NFS fonctionne sur OSX, la doc de Vagrant nous dit clairement que le mode NFS n’est pas disponible sur Windows.

J’ai donc commencé par complètement désinstaller XDebug. Ça n’a rien changé. Ou si, peut-être ai-je gagné 100ms.

Ensuite, j’ai effectué la modification du fichier `AppKernel.php` pour déplacer les dossier `cache` et `logs` vers un dossier non synchronisé de la machine virtuelle, comme suggéré sur le billet de blog précédemment cité. Cela m’a fait gagner 500ms à 1 seconde. Pas mal, mais sur des temps de chargement de 4-5 secondes, ça ne change pas grand chose, et ça reste toujours très lent.

## [](#et-la-solution)…et LA Solution

Alors comment on fait quand on est sur Windows et qu’on veut utiliser Vagrant pour développer, sans sacrifier sa santé mentale à attendre 5 secondes entre chaque rafraîchissement ?

On n’écoute pas la documentation ! Celle de Vagrant, en tout cas. En réalité, le mode NFS sous Windows est disponible, mais uniquement à l’aide d’un fantastique petit plugin pour Vagrant nommé [Winnfsd](https://github.com/GM-Alex/vagrant-winnfsd).

Pour l’installer, rien de plus simple. Sur votre machine hôte, lancez la commande:

```
vagrant plugin install vagrant-winnfsd
```

Puis dans votre fichier `VagrantFile`, ajoutez l’option `nfs` à ligne qui configure le dossier partagé:

```
config.vm.synced_folder "./", "/var/www", type: "nfs"
```

Si votre machine est déjà lancée, relancez-la avec `vagrant reload`. Et c’est tout.

Au lancement de la machine virtuelle, vous allez avoir une demande d’autorisation pour le pare-feu Windows. Pensez à bien accepter. J’ai eu un problème au départ, le dossier ne se montait pas dans la machine virtuelle, à cause d’un problème de pare-feu (au lancement de la machine, le process figeait à l’étape de montage des dossiers synchronisés. Mettre à jour le pare-feu a permis de débloquer cette étape).

## [](#le-resultat)Le Résultat

Le résultat est sans appel: le même site sous Symfony qui auparavant prenait 8-10 secondes au premier chargement (sans cache), prend maintenant 3-4 secondes. Et avec le cache, c’est **rapide comme l’éclair**, avec un temps de chargement de la page de **300-500ms en moyenne**, toujours en mode `dev`.

En réalité, vous pouvez gagner encore plus, avec les modifications précédentes (désactiver XDebug, changer l’emplacement des fichiers de cache et de logs), mais bon, je suis passé de 4 secondes à 500ms, ça me suffit largement. Les pages se chargent instantanément, c’est un vrai bonheur !

![Temps de chargement Symfony2 après](images/2014-07-22_19.32.36.png)
