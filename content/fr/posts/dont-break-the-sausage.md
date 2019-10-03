---
title: "Don't Break The Sausage"
date: 2019-09-16T12:47:45+02:00
author: "Clément Fazilleau"
draft: false
categories: ["Project"]
tags: []
description: dont-break-the-sausage
---

## Don't Break The Sausage

est un jeu que j'ai créé à l'occasion de la "game week" de mon école.

J'étais dans une équipe composée de 2 programmeurs, 1 game designers, 3 artistes et 2 sound designers.

{{< youtube jDkyII-2-qI >}}

Mon principal défi sur ce projet était la physique de la saucisse et du pain.

J'ai commencé par faire un script qui crée des game gameObjects avec des colliders 2D, des rigidbody et des hinge joints attachés les uns aux autres.
J'ai ensuite généré une courbe de Bézier parcourant tous ces gameObjects. J'ai ensuite utilisé cette courbe pour créer un mesh 2D pour la saucisse. De cette façon, le mesh est lisse et beau même si la saucisse est tordue.

{{< zooom src="/dont-break-the-sausage/dev.png" >}}

Cette technique que j'ai utilisé fonctionne bien, mais il existe d'autres options, comme utiliser un shader de post-process au lieu de générer un mesh, mais pour les plateformes mobiles, la prise en charge du post-process dépend en grande partie de l'appareil et j'ai choisi de privilégier la stabilité plutôt que les performances.

{{< zooom src="/dont-break-the-sausage/sidebyside.png" >}}

Don't break the sausage a reçu le prix de l'originalité à la fin de la semaine et s'est vu offrir la possibilité d'être publié par Webedia games.

{{< image src = "/dont-break-the-sausage/award.png" >}}
