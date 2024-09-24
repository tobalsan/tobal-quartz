---
title: "Annuler simplement et rapidement un commit sur GIT"
date: "2016-02-02"
tags:
  - "code"
coverImage: "code-git.jpg"
---

Si vous utilisez GIT comme gestionnaire de version et que, pour une raison ou une autre, vous soyez allé un peu trop vite en besogne en faisant un `git commit`, pas de panique, voici une solution toute simple pour annuler votre commit sans perdre vos modifications. Il vous suffit de taper (en ligne de commande):

```
git reset --soft HEAD^
```

Vous vous retrouverez à l'état juste _avant d'avoir commit_, mais avec votre espace de travail conservé avec les toutes dernières modifications. Donc, si vous ajouter par exemple des nouveaux fichiers, vous devrez faire

```
git add .
```

et vous pourrez faire un nouveau commit.
