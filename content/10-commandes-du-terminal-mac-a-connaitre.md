---
title: "10 commandes du terminal Mac à connaitre"
date: "2016-12-06"
tags:
  - "applications"
  - "astuces"
  - "mac"
coverImage: "terminal.jpg"
---

Un des outils les plus puissants - mais également parmi les plus méconnus - sur Mac est sans conteste **le Terminal**. Étant basé sur le noyau Unix (qui est aussi la base des systèmes d'exploitation Linux), Mac OS X incorpore donc cet outil qui vous permet de réaliser vraiment tout et n'importe quoi en ligne de commande, et surtout bien plus de choses que depuis n'importe quelle interface graphique, plus rapidement et, je vous l'assure, plus facilement.<!--more-->

Et si la ligne de commande vous donne des boutons (ah ah ! Hum...), rassurez-vous, ce n'est pas si compliqué que ça. Je vais d'ailleurs vous le prouver en vous faisant découvrir 10 commandes fort pratiques mais qui restent simple: elles font toutes pour la plupart une seule ligne. Un simple copier-coller, et vous êtes bons.

## 1\.  Redémarrer automatiquement votre Mac quand il plante / freeze

```
sudo systemsetup -setrestartfreeze on
```

Cette commande va vous permettre de paramétrer votre Mac afin qu'il redémarre automatiquement en cas de freeze. Évidemment, cette commande est à rentrer avant que votre Mac ne plante, mais il suffit de l'entrer une seule fois pour que ce soit effectif à l'avenir.

## 2\. Afficher les dossiers et fichiers cachés

```
defaults write com.apple.finder AppleShowAllFiles -bool true
```

La commande ci-dessus va forcer le Finder à afficher tous les dossiers et fichiers cachés présents sur votre Mac. Que ce soit pour chercher dans des fichiers systèmes (faites attention à ce que vous faites tout de même), ou bien repérer des fichiers fantômes qui prennent de la place, cela peut servir.

## 3\. Désactiver la confirmation de suppression

![](images/confirmation-suppression.png)

```
defaults write com.apple.finder WarnOnEmptyTrash -bool false
```

Si vous supprimez souvent des fichiers et aimez aussi souvent vider la corbeille, cette commande désactive le petit message de confirmation qui vous demande systématiquement si vous êtes bien sûr de vouloir vider la corbeille. Désormais, dès que vous cliquerez sur "Vider la corbeille", l'action sera instantanée.

## 4\. Faites parler votre Mac

Le text-to-speech vous connaissez ? C'est une fonctionnalité sympa qui permet à votre ordinateur de parler. Et pour cela, pas besoin d'installer de logiciel, OS X sait le faire de base. Il vous suffit de lancer un terminal, et de taper la commande "say" suivie du texte à énoncer, comme ceci:

```
say votre texte blabla
```

## 5\. Activer AirDrop sur les anciens Mac

Personnellement, je ne me sers pas d'AirDrop, mais si c'est votre cas, et que vous disposez d'un Mac ancien , utilisez la commande suivante dans le terminal pour activer AirDrop:

```
defaults write com.apple.NetworkBrowser BrowseAllInterfaces -bool TRUE
```

## 6\. Reconstruire l'index Spotlight

![](images/spotlight.png)

Afin de pouvoir vous proposer tous les résultats de recherche en temps réel, Spotlight doit indexer le contenu de vos disques durs. Parfois, il peut être nécessaire de réinitialiser et reconstruire cet index (si il ne s'est pas mis à jour par exemple). Ce n'est pas quelque chose que vous devriez être amené à faire souvent mais si jamais c'est le cas, vous saurez comment faire.

```
sudo mdutil -E /
```

Vous devrez entrer votre mot de passe pour valider l'action.

## 7\. Activer la sélection de texte dans Quick Look

Quick Look est une fonction bien pratique d'OS X qui vous permet de visualiser le contenu d'un fichier depuis le finder, sans avoir besoin de l'ouvrir, simplement en appuyant sur la barre d'espace quand celui-ci est sélectionné. Cependant, par défaut, vous ne pouvez pas sélectionner le texte des fichiers texte et PDF. Afin d'activer cette fonctionnalité, entrez cette commande dans le terminal:

```
defaults write com.apple.finder QLEnableTextSelection -bool TRUE
```

## 8\. Empêcher votre Mac de se mettre en veille

Il peut arriver que vous ayez besoin de maintenir votre Mac éveillé, même si vous ne vous en servez pas. Par exemple lors d'un téléchargement un peu long. Pour cela, rien de plus simple, utilisez la commande:

```
caffeinate
```

et c'est tout. Rien besoin d'ajouter. Cette commande va maintenir votre Mac en état actif pour ne pas qu'il passe en mode veille tout seul.  _Note: bizarrement, le comportement de cette commande semble aléatoire. Si votre Mac se met toujours en veille malgré tout, vous pouvez utiliser l'application [Caffeine](https://itunes.apple.com/us/app/caffeine/id411246225?mt=12), simple mais qui fait parfaitement le boulot._

## 9\. Désactiver le Dashboard

![](images/osx-dashboard.jpg)

Si, comme moi, vous ne vous servez jamais du Dashboard (l'écran virtuel où sont tous les widgets), alors désactivez-le ! Il vous suffit d'entrer la commande:

```
defaults write com.apple.dashboard mcx-disabled -boolean YES
```

Apple a annoncé que le Dashboard serait de toute façon désactivé dans les prochaines versions d'OS X. Et en attendant, si jamais vous changez d'avis, il suffit d'entrer à nouveau cette commande en remplaçant le "YES" par un "NO".

## 10\. Voir l'historique des commandes

Pour finir, voici une petite astuce bien pratique: une commande pour lister l'historique des dernières commandes entrées. Bien pratique pour éviter d'avoir à aller chercher des commandes longues ou complexes qu'on a entrées dans le passé. Tapez:

```
history
```

validez, et c'est tout !

## Conclusion

Vous voyez, le terminal est un outil extrêmement puissant et qui permet de faire tout un tas de choses bien pratiques. Et ce que nous venons de voir n'est qu'une infime partie des possibilités ! Bien qu'il puisse paraitre complexe de premier abord, en se forçant un peu à l'utiliser, on se rend vite compte qu'il n'est pas si dur que ça et que ça vaut le coup de s'y mettre.

Et vous, connaissez-vous d'autres commandes à la fois simples et bien pratiques comme celles-ci ? Si oui, n'hésitez pas à les partager avec nous dans un commentaire :)

Source: [MakeTechEasier](https://www.maketecheasier.com/mac-terminal-commands/)
