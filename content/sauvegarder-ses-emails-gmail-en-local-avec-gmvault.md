---
title: "Sauvegarder ses emails Gmail en local avec Gmvault"
date: "2016-03-01"
tags:
  - "astuces"
coverImage: "sauvegarder-emails-gmail-gmvault.jpg"
---

Gmail, j'adore. Je m'en sers tous les jours, toutes les heures.

J'ai même plusieurs comptes d'ailleurs. Et un jour, comme ça sans prévenir, Google a complètement bloqué l'un deux. Plus aucun accès, plus le droit de se connecter ni même de récupérer les emails présents dans la boite.<!--more-->

Et c'est là que je me suis rappelé le dicton rabâché par l'ami [Korben](http://korben.info/):

> Tout ce que vous mettez sur le net ne vous appartient plus.

Bon, c'est un peu extrême mais pour le coup, c'est on ne peut plus vrai. Fort heureusement ce n'était pas ma boite principale.

C'est alors que j'ai recherché une solution permettant de rapatrier tous les emails de mes comptes Gmail facilement et rapidement. Alors il y a plusieurs méthodes, on peut par exemple utiliser Thunderbird et tout récupérer en POP.

Mais je voulais quelque chose de rapide, d'immédiat, genre un gros bouton "Télécharger vers" qui me permette de stocker tous mes emails dans un dossier sur mon ordinateur.

C'est là que je suis tombé sur [Gmvault](http://gmvault.org/).

Gmvault est une application légère et rapide qui va vous permettre de sauvegarder vos emails Gmail en les téléchargeant directement sur votre disque dur.

Alors il n'y a pas de gros bouton "Télécharger". Il n'y a d'ailleurs aucun bouton puisqu'il s'agit d'une application en ligne de commande. Non ne vous enfuyez pas, je vous assure, c'est très très simple à utiliser et je vais vous montrer comment faire. C'est facile et ça prend 5 minutes.

**Mise à jour**: Si vous êtes plus vidéo, je vous ai fait un petit tuto en vidéo sur Youtube:

<iframe src="//www.youtube.com/embed/I_MIVTvjaHM" width="630" height="473" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

## [](#pr%C3%A9paration)Préparation

Vous devez vous assurez que votre compte Gmail autorise la connexion en IMAP. Allez sur votre boite Gmail, dans les options puis sur **Transfert et POP/IMAP** et vérifiez que IMAP est bien activé. Assurez-vous aussi que l'option **Limites de taille des dossiers** est bien sur "Ne pas limiter...".

Ensuite, allez dans la gestion des libellés et assurez-vous que les cases "Afficher en IMAP" pour **Tous les messages** et **Tous les chats** soient cochées.

## [](#installation)Installation

[Téléchargez l'installateur de Gmvault](https://bitbucket.org/gaubert/gmvault-official-download/downloads/gmvault_installer_v1.8.1-beta.exe) puis lancez-le.

Vous pouvez l'installer n'importe où ça n'a pas d'importance. Par défaut, le programme va vous créer un raccourci sur le bureau. Utilisez-le pour lancer Gmvault. Vous devriez avoir une invite de commande.

Vous avez presque fini !. Il vous suffit simplement de tapez la commande suivante: `gmvault sync votreadresse@gmail.com`

en remplaçant bien sûr `votreadresse@gmail.com` par votre vrai email. Appuyez sur Entrée, et Gmvault va écrire un long message.

Il vous indique uniquement qu'il a besoin de votre autorisation pour se connecter à votre compte Gmail, puisque vous à aucun moment vous ne donnez votre mot de passe.

Appuyez à nouveau sur Entrée, une fenêtre de navigateur doit s'ouvrir automatiquement. Il s'agit d'une page où Google demande l'autorisation de laisser Gmvault récupérer vos emails. Cliquez donc sur "Autoriser" et vous pouvez fermez la fenêtre.

Revenez dans la console et appuyez sur Entrée une nouvelle fois. Gmvault va alors se connecter et lancer la récupération de votre boite Gmail complète.

_Petite note pour les utilisteurs de l'antivirus gratuit Avast: vous devrez désactiver l'agent Mail de Avast avant de commencer la sauvegarde sinon Gmvault ne parviendra pas à récupérer vos emails_.

Tous vos emails seront sauvegardés dans votre dossier utilisateur, dans le dossier **gmvault-db**. L'outil est assez rapide, mais si vous avez plusieurs gigaoctets de mails comptez quand même une heure ou deux.

Sachez que cela fonctionne également pour les utilisateurs de Google Apps. Que du bonheur.
