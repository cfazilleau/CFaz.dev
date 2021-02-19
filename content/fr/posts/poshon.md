---
title: "Poshon"
date: 2020-03-15
author: "Clément Fazilleau"
draft: false
categories: [ Project ]
tags: [ Game, Unity, Switch ]
description: A switch game created during a R&D (Research and Development) project.
---

Poshon est un jeu de coopération en multijoueur local créé lors d'un projet de R&D par mon ami Julien Soysouvanh et moi même.
Cet article portera surtout sur le jeu en lui-même, mais si vous souhaitez plus d'informations sur le processus de développement, vous pouvez lire mon article sur [une première expérience avec le devkit switch] (/fr/posts/a-first-experience-with-the-switch-devkit).

## Le jeu

Ce jeu est très inspiré de [*overcooked*](http://www.ghosttowngames.com/overcooked/). Notre intention était de créer un jeu multijoueur local jouable avec jusqu'à 8 joueurs et sur la même console en utilisant les joycons et leurs fonctionnalités spécifiques, comme le gyroscope, par exemple.

Tout le gameplay repose sur vitesse et coordination. Les potions demandées apparaîtront sur la droite de l'écran et les joueurs devront les recréer dans le bon ordre le plus rapidement possible.

<div style="text-align:center;"><i>Vidéo à venir</i></div>

## Attributs de potions

- Couleur:

Vous devrez créer des potions de la bonne couleur en mélangeant différents liquides à partir des multiples robinets disposés dans le niveau.

- Type:

Les différents types de potions disponibles sont "normaux", "pétillants" ou "toxiques", ils sont représentés par les particules au-dessus du flacon. Chaque fois que vous mélangez différentes potions, le type est réinitialisé, alors faites attention à choisir la couleur de votre potion avant le type, sinon vous perdrez de précieuses secondes. Le type est défini à l'aide de la table correspondante (pétillant ou toxique).

- Temps de distillation:

Le temps de distillation est indiqué par le petit nombre à droite de la potion, il est réglé à l'aide de la table de distillation, en y disposant la potion durant un certain temps, mais attention à ne pas la laisser trop ou pas assez longtemps.

{{<zooom src = "/poshon/Interactions.png">}}

## Temps

Sur chaque carte, vous disposez d'un certain temps pour compléter une liste de potions générées aléatoirement. chaque potion doit être complétée dans le bon ordre, et les points que vous obtenez pour chaque potion sont basés sur la précision de la recette (couleur, type, temps de distillation ...).

## Joueurs

Dans le menu de sélection de la carte, vous pouvez ajouter jusqu'à 8 joueurs.

{{<zooom src = "/poshon/LevelSelect.png">}}

## Maps

nous avons créé 4 maps, la première est une carte d'entraînement, où vous pouvez faire un nombre infini de potions en un temps infini. La deuxième carte est simple, pour 1 à 8 joueurs. la troisième est une carte divisée en deux où vous devez être au moins deux joueurs (un de chaque côté) et vous pouvez vous partager des potions en les posant sur des tapis roulants et sur les tables. la dernière carte est une carte de minimum 4 joueurs, qui est divisée en 4 "cellules". afin de partager des potions, vous devez les déposer sur le tapis roulant.

{{<zooom src = "/poshon/Maps.png">}}
{{<center text="Un projet par Julien SOYSOUVANH et Clément FAZILLEAU">}}
