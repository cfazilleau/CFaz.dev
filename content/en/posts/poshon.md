---
title: "Poshon"
date: 2020-03-15
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: [ game ]
description: A switch game created during a R&D (Research and Development) project.
---

Poshon is a multiplayer couch game created during a R&D project by my friend Julien Soysouvanh and myself.
This post will be especially about the game in itself, but if you want more informations about the devlopment process, you can read my article about [a first experience with the switch devkit](/posts/a-first-experience-with-the-switch-devkit).

## The game

This game is very inspired by [*overcooked*](http://www.ghosttowngames.com/overcooked/). We wanted to create a local multiplayer game playable with up to 8 players at the same time and on the same console using the joycons.

All the gameplay is about speed and coordination. The potions requested will appear on the right of the screen and you'll have to recreate them in the good order as fast as possible.

<div style="text-align:center;"><i>Video coming soon</i></div>

## Potions Attributes

- Color:

You'll have to create potions of the good color by blending between different liquids from the multiple faucets on the map.

- Type:

The different types of potion available are "normal", "sparkling", or "poisonous", they are reprensented by the particles above the flask. Every time you are blending different potions, the type is reset, so be careful to choose the color of your potion before the type, or you'll lose precious seconds. The type is set using the accurate table (sparkling of poisonous).

- Distillation time:

The distillation time is shown by the little number on the right of the potion, it is set using the distillation table, and by waiting the corresponding time, be careful of not leaving it for too long or not enouh time.

{{< zooom src="/poshon/Interactions.png" >}}

## Time

On each map, you have a certain amount of time to complete a list of randomly generated potions. every potion has to be completed in the good order, and the points you get for each potion are based on the accuracy of the potion's recipe (color, type, distillation time...).

## Players

On the map selection menu, you can join up to 8 players to help you in the making of all the potions.

{{< zooom src="/poshon/LevelSelect.png" >}}

## Maps

we created 4 maps, the first is a training one, where you can make an infinite number of potions in an infinite amount of time (27 days). The second map is a simple one, for 1 to 8 players. the third one is a map splitted in two where you have to be at least two players (one on each side) and you can share potions by passing them on the conveyor belts and over the tables. the last map is a 4 players minimum map, which is divided into 4 "cells" in order to share potions, you have to drop them on the conveyor belt.

{{< zooom src="/poshon/Maps.png" >}}
