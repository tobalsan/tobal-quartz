---
title: "Empêcher Windows 10 de s'allumer tout seul la nuit"
date: "2016-12-13"
tags:
  - "astuces"
coverImage: "windows-update-ordinateur-s-allume-tout-seul.jpg"
---

Depuis que je suis passé à Windows 10, je me suis aperçu que régulièrement (au moins une fois par semaine), mon ordinateur s'allumait tout seul la nuit. Je faisais bien attention à l'éteindre avant d'aller dormir et, le lendemain matin, je le retrouvais allumé. Au début je me demandais si c'était moi qui avais la mémoire qui flanche. J'ai des chats mais ça ne pouvait pas être eux étant donné que je ferme systématiquement la porte de mon bureau et, à ce jour, ils ne savent pas encore ouvrir et refermer les portes.

Mais au bout de 4-5 fois, je me suis dit que j'allais regarder sur internet quand même. Et là je suis tombé sur pleins de gens à qui ça arrivait aussi. Youpi, je ne suis pas le seul ! Mon ordinateur n'est pas possédé par un quelconque fantôme ou esprit joueur. Donc si votre PC souffre également d'insomnie, j'ai trouvé la solution pour vous.<!--more-->

## Le problème

En réalité, c'est dû à un paramètre par défaut de Windows 10, qui permet à votre ordinateur de sortir de veille si des mises à jours sont disponibles afin de les installer immédiatement. Le terme "veille" est vague, car en fait, peu importe que votre ordinateur soit en veille ou carrément éteint, si une mise à jour est disponible, il s'allumera. Par défaut, le "réveil" est programmé à 2 heures du matin pour que les mises à jour se déroulent pendant que vous dormiez, afin de ne pas vous gêner. Le souci, c'est que le PC ne se ré-éteint pas ensuite.

Bof bof pour les économies d'électricité et la protection de l'environnement !

## La solution

La solution à ce problème, c'est de simplement désactiver ce paramètre qui est donc activé par défaut. Pour cela, rendez-vous dans le **Panneau de configuration > Système et sécurité > Sécurité et maintenance** (cliquez directement sur le titre de section, en vert):

![](images/systeme-securite-maintenance.png)

puis déroulez le panneau **Maintenance**, cliquez sur **Modifier les paramètres de maintenance**, et enfin décochez la case **Autoriser la maintenance planifiée de manière a interrompre la veille de mon ordinateur**.

![](images/parametres-maintenance-automatique.png)

![](images/desactiver-maintenance-automatique.png)

Validez en appuyant sur **OK** et vous êtes bon ! Votre PC ne se réveillera plus en plein milieu de la nuit et vous pourrez dormir tranquille.
