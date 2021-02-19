---
title: "Slide Slide Little Penguin!"
date: 2019-05-19
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: [ game, "Mobile", "Unity" ]
description: A small mobile game made as a math project...
---

## Slide Slide Little Penguin

is a small mobile game created as a mathematical project. The goal of this project was to create a "clone" of *Tiny Wings* or *Dune* and thus to procedurally generate an infinite 2D terrain and to program the physics applying to it.
The secondary objective of this project was to create an optimized and stable mobile game.

{{< youtube lp4QMA8zNrQ >}}

*recording from my phone wasn't as good as I expected.*

------------

## The game

The main problem for this kind of game is to create an infinite terrain in a procedural way, and in real time without affecting the performances.
To solve this problem, we have to organize our terrain in different portions of curves, aligned the ones with the others in order to create random "hills" on which our character will slide to go as far as possible in a small time.

## Display

the terrain rendering is done in post processing, by calculating points on the curve relative to the screen, by doing that, rendering 5 or 5000 curves will not present any difference in performance. In addition, parts of curves outside the screen will never be rendered.

This type of render is interesting because it avoids generating meshes or splines in real time, which would have been much more expensive in performance, and it also allows us to create really custom physics very simply.

{{< zooom src = "/slide-slide-little-penguin/editor.png" >}}

## Physics

The physics created for this game are totally custom and optimized, which made it possible to avoid the physics and colliders system of unity, whom would have been much too exaggerated for the kind of game wanted, the terrain being generated procedurally.

The physics works actually using just the position and velocity of the player and the position and tangent on the curve directly under it. This way the physics won't check the rest of the terrain, which would be useless knowing that the player is the only dynamic entity of the game.

---------------

<div align = "center"> A project by Julien SOYSOUVANH and Clément FAZILLEAU </div>