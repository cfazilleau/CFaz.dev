---
title: "Une première expérience avec le devkit switch"
date: 2020-03-15
author: "Clément Fazilleau"
draft: false
tags: [ game, switch ]
description: Un projet de recherche et développement sur le devkit de la switch.
---

Au cours de ma troisième année à ISART, j'ai eu l'opportunité de réaliser un projet de 2 semaines en utilisant le Devkit Nintendo Switch. Ce n'est pas une occasion fréquemment donnée aux étudiants, alors mon ami Julien et moi-même avons saisi cette opportunité. Voici ce que nous avons appris:

> Cet article est un résumé du document que nous avons dû écrire sur notre experience avec le devkit de la Nintendo Switch. Comme vous vous en doutez, une grande partie de ce que nous avons appris était strictement confidentiel et sous la protection d'un accord de confidentialité (NDA) avec Nintendo. Si vous lisez ceci en esperant de trouver des informations privées apropos du devkit et des logiciels utilisés, vous ne trouverez rien sur cette page. Ceci étant dit, allons-y.

Vous pouvez également lire l'article sur [Poshon, le jeu que nous avons créé pendant ce projet.](/posts/poshon)

## Pourquoi ce choix R&D

Nous avons choisi ce projet de recherche et développement en premier lieu pour l'opportunité qui nous est donnée.

Travailler sur Nintendo Switch est un privilège que nous ne sommes pas sûrs d'avoir à l'avenir et c'était l'occasion de voir et d'utiliser des outils professionnels de consoles sous licence.

C'était aussi un défi personnel puisque nous avions pour objectif de développer un jeu complet, pendant les deux seules semaines du projet.

Le choix du moteur Unity a été fait car nous voulions découvrir à la fois les packages du nouvel Input System ainsi que la Universal Render Pipeline (mais la version d'Unity étant trop ancienne, nous avons dû nous rabattre sur la Lightweight Render Pipeline). Ce moteur nous a également permis de réaliser un prototypage rapide et simple.

<img style = "height: 100px; margin: auto;" src = "https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Unity_Technologies_logo.svg/1280px-Unity_Technologies_logo.svg.png"> </img>

## Nos objectifs

L'objectif que nous nous étions fixé pour ce projet était de développer un jeu complet sur l'unité 2019 en apprenant et en utilisant les fonctionnalités suivantes:

- Les joycons.

Ce sont les manettes de la switch. Avec la possibilité de connecter jusqu'à huit sur la même machine, nous nous sommes concentrés sur le gameplay multijoueur local, prenant en charge un maximum de huit joueurs. Les contrôleurs sont également equipés de gyroscopes, une fonctionnalité que nous avons utilisée dans notre jeu.

- La Lightweight render pipeline (LWRP).

Il s'agit d'un package encore en preview qui est apparu avec la version 2019.1 d'Unity, il a été créé pour obtenir plus de performances que la pipeline de rendu classique sur des plates-formes telles que les mobiles ou les machines avec une configuration faible. Nous avons fait ce choix en fonction des performances offertes par la console, proche de celle d'un smartphone haut de gamme.

- Le package "Input System".

Destiné à remplacer l'actuel input manager du moteur, nous avons utilisé cet outil, bien qu'il soit toujours en preview, pour connaître ses spécificités et ses faiblesses.

<img style = "height: 150px; margin: auto;" src = "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/Nintendo_Switch_Logo.svg/800px-Nintendo_Switch_Logo.svg.png"> </img>

## Matériel

> J'ai choisi de garder cette partie privée car elle contenait principalement des informations confidentielles de Nintendo sous la protection d'un NDA (Non-Disclosure Agreement).

## Devkit et SDK

> J'ai choisi de garder cette partie privée car elle contenait principalement des informations confidentielles de Nintendo sous la protection d'un NDA (Non-Disclosure Agreement).

## Performances et débogage

> J'ai choisi de garder cette partie privée car elle contenait principalement des informations confidentielles de Nintendo sous la protection d'un NDA (Non-Disclosure Agreement).

## Joycons

> J'ai choisi de garder cette partie privée car elle contenait principalement des informations confidentielles de Nintendo sous la protection d'un NDA (Non-Disclosure Agreement).

## Lightweight Render Pipeline

La Lightweight Render Pipeline (ou LWRP) est un package Unity utilisant les nouveaux «Scriptable render pipelines» (ou SRP) et est optimisé pour les machines à faibles performances telles que les mobiles.

C'est à partir de cette observation que nous avons choisi de l'utiliser pour le switch, De plus, son opposée, la High Definition Render Pipeline (ou HDRP) était trop puissante et exigeante en ressources, et il aurait été inutile de choisir une aussi grosse fonctionnalité, et il aurait même été risqué de faire ce choix et de se retrouver au milieu du projet à devoir recibler le projet sur la LWRP, et à recréer tous les matériaux, shaders et autres ressources spécifiques au rendu.

la LWRP étant basique, nous avons toujours utilisé une grande quantité de ses fonctionnalités, telles que l'anti-aliasing, les ombres, les matériaux dynamiques, les shaders (créés à partir du nouveau "Shader Graph") ou les effets de post-process tels que "Vignette", "Bloom", et "Color Correction".

{{< zooom src="/a-first-experience-with-the-switch-devkit/LWRPSettings.png" >}}

## Input System

L'Input System est un package disponible depuis Unity 2019.1, en version 1.0.0-preview-4 lors de notre projet. Il était risqué de l'utiliser, étant donné son instabilité. Nous l'avons cependant utilisé dans un premier temps pour apprendre a l'utiliser, mais aussi parce que son implementation des joycons était très accessible et cross-plateform, nous permettant de tester notre jeu depuis nos PC, en utilisant des contrôleurs Xinput classiques.

Le but de ce package est de standardiser les entrées autant que possible, via des control schemes (schémas de liaison à un "appareil" spécifique) ou des Player Input Components (composant utilisé pour transmettre les inputs d'un appareil à un gameobject, de cette manière, un objet A ne recevra que les inputs d'un contrôleur A et un objet B ne recevra que les inputs d'un contrôleur B). Ce package permet également la prise en charge directe de plusieurs appareils et peripheriques personnalisés.

Le principal problème rencontré dans l'Input System est l'instabilité de ce package. Il fonctionne parfaitement dans une partie solo, mais est plus complexe en multijoueur, par exemple, en contrôlant l'UI à partir de plusieurs contrôleurs, ou lors de l'ajout de joueurs. Le code de ce package était également relativement peu documenté, et certaines méthodes ne sont pas encore implémentées.

{{< zooom src="/a-first-experience-with-the-switch-devkit/InputActions.png" >}}

## Autres caractéristiques

> J'ai choisi de garder cette partie privée car elle contenait principalement des informations confidentielles de Nintendo sous la protection d'un NDA (Non-Disclosure Agreement).

## Conclusion

Nous avons beaucoup appris grâce à ce projet, et avons découvert de grandes contraintes, qui ont finalement été facilement surmontées grâce à Unity (et son Input System)

Ce fut très agréable de travailler sur Unity, pour son temps de compilation rapide, son temps de "build" relativement bas, la simplicité de son architecture, et grâce aux packages utilisés. Le même jeu utilisant le moteur Unreal aurait ~~probablement~~ nécessité (beaucoup) plus de temps.

Les ressources utilisées ont été trouvées sur Internet / l'asset store, ou modélisées ou dessinées par nous memes, malgré l'absence de Game Designers, Artists ou Sound Designers, le résultat est très amusant et le jeu est largement jouable.

{{< zooom src="/a-first-experience-with-the-switch-devkit/Poshon.png" >}}
