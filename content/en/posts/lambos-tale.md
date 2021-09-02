---
title: "Lambo's Tale"
date: 2020-06-02
author: "Clément Fazilleau"
draft: false
categories: [ Project ]
tags: [ Game, Unity ]
description: A 2D metroidvania created for my third year at ISART.
---

## Introduction

Lambo's Tale is a 2D platformer implementing Metroidvania mechanics.
It was created as an end of third year project in just over four weeks in the company of 3 very good programmers, 4 wonderful designers and 3 talented artists (all names are cited at the end of the article).

<div align="center"><iframe frameborder="0" src="https://itch.io/embed/760286?linkback=true&amp;bg_color=222222&amp;fg_color=eeeeee&amp;border_color=363636" width="552" height="167"><a href="https://cfaz.itch.io/lambos-tale">Lambo's Tale by cfazilleau</a></iframe></div>

The rather unexpected specificity of this project is the fact that it was carried out entirely remotely, due to the containment linked to Covid-19. Despite this inconvenience, good internal communication within the group as well as the efforts made by each member of the team made it possible to carry out this project.

{{<youtube 6GjfYDQagJo>}}

The game tells us the story of Lambo, a little lamb who goes to fight packs of wolves in order to avenge his sister, Lambette.
He will have to go through various levels and will collect golden eggs which will allow him to buy new abilities in order to increase his skills (health, resistance, attack).
In each level there is also an arena, called "Wolf's Den" which will allow us to gain new attacks by fighting all the enemies.

At the end of a level, we will find a book that will allow us to move on to the next. There are three levels in all, with the first two being procedurally generated.

{{<zooom src="/lambos-tale/Screenshot_04.PNG">}}

## Technical specifications

The game was developed on Unity 2019.3.7f1, which allowed us to use specific features (especially in 2D), such as:

- **Universal Render Pipeline** which allowed us to create shaders using the Shader Graph, which has been found to be quite useful for creating this type of mixed rendering between 2D and 3D.
- **2D Collisions**, although the rendering is in 3D, the collisions are performed in 2D, in order to support tilemaps, and obtain better performance.
- **2D Grid / Tilemaps** which are used by procedural generation to create levels.
- **Rule Tiles** which are used to connect the tiles together and achieve this smooth terrain effect. they also allow us to generate "3D" tiles.
- **Platform effector 2D** used for one-way platforms
- **PSD importer** which lighten the workload for artists and allow us to quickly implement textures and sprites.
- **Scriptable objects** which are used to store data on skills, abilities, shop items, etc ...

C# Scripting in Unity allowed us to iterate and test our functionalities quickly and efficiently, which is a significant point given the scope of the project. The use of this engine also allowed us to have access to different packages:

- **Cinemachine** was used for all camera effects, it is an accessible tool that allowed us to create an intuitive camera and perfectly match this type of dynamic platformer.

- **Animancer** is a plugin that allowed us to precisely control the animations of all the characters in the game, the combat system being extremely precise, the use of unity animations would have been chaotic to put in place. place, and would have had too big an impact on performance.

- **Input System**, this new input management system is intended to replace the current Unity Input Manager. we wanted to use it in order to train ourselves a little more on this tool. The basic inputs would also have required a significant code base, or manual bindings which would have been detrimental to the architecture of our project.

{{<zooom src="/lambos-tale/Screenshot_03.PNG">}}

## Features

#### Player Controller

The player controller required the following features:
- simple movement
- jump
- wall-jump
- wall-slide
- dash (in the style of "Celeste")

In order to have a pleasant feeling and allow designers to easily tweak the various parameters, the following technology choices have been made:
The Player Controller uses a simple 2D Rigidbody as well as a 2D Box Collider, to be able to benefit from Unity's physics and collision resolution, however, the player's velocity is fully calculated in this script to keep full control over all movements.

The controller also benefits from:
- Coyote time, allowing the player to jump a few milliseconds after falling from a platform.
- Jump buffering, allowing the player to easily perform "frame-perfect jumps"
- Snapping, when the player hits a corner of a wall, the game will try to modify the player's trajectory in order to avoid the wall.

These three features are present in the game "Celeste", which was a great source of inspiration for our project. you can find more information about these features [here](https://twitter.com/MattThorson/status/1238338574220546049).

The different states of the controller were managed via a simple HFSM (Hierarchical Finite State Machine) pattern, using a universal transition system, in order to allow easy addition of new states.
however, the weakness of this system is the cause of potential invalid state transition bugs, which would have been more easily avoided or fixed using another design pattern.

{{<zooom src="/lambos-tale/Screenshot_05.PNG">}}

#### Input buffer

The auto-combo system for combat required the use of an input buffer to allow the player to smoothly trigger and cancel attack animations.
the input buffer records the last X actions by keeping in memory the timestamp of its triggering. The controller can then "consume" the inputs and choose to validate them or not, depending on its state.

The buffer used is a circular buffer, in order to reduce the runtime allocations as much as possible and always keep a fixed memory size.

#### Procedural Generation

Each level is generated procedurally (via 2D tile grids) to make sure that each level will be different, however, it is possible for Game Designers to create portions of levels that will not be affected by the procedural generation. For this purpose, the generator must use both random and pathfinding algorithms, implemented here via a simple A* algorithm. This algorithm will make it possible to join the various specified constraints, and a budget system will make it possible to make a more or less linear plot.
Once the path is built, random rooms are assigned to it according to constraints on their openings (right / left / up / down). In order to add even more randomness, each room design contains random elements (enemies / obstacles / bonuses ...) controlled by probabilities set by the game designers.

{{<zooom src="/lambos-tale/Screenshot_10.png">}}

#### Combat system

when the player attacks or uses an ability, the character transitions to the corresponding state, canceling any state of no combat to play the corresponding animation and trigger the events specific to many fighting games:

- Startup (most animations can be canceled in this state)
- Active (application of the attack, cannot be canceled)
- Recovery (the character cannot move)
- End (control is regained)

These events are used to control the behavior of attacks and their hitboxes. it is particularly important in our case since the input buffer makes it possible to chain attacks (auto combo) which implies that the framedata is as precise as possible.
Given the variety of attacks and abilities, animations should be easily editable and have enough different settings.

#### Items

Different items can be picked up by the player (health bonus, keys, currency, skills), and some items must be able to be added during production. This is the reason why the code architecture should be very flexible on this point.
all the "pickables" therefore inherit from a class implementing the behavior of "Pick". There are several kinds of pickable, for example, some are made to be stored (like capacities for example) and others must be instantly consumed (health).
In a single level, there can be hundreds of pickables at the same time, which is why a pooling system has been implemented for the items.

{{<zooom src="/lambos-tale/Screenshot_02.PNG">}}

#### Platforms

The level-design will contain one-way platforms through which the player can pass, but only in one direction (from bottom to top). Unity's "Platform effector 2D" component was created for this behavior. These platforms also have specific physical settings in order to avoid unexpected behavior (wall jump, slide, etc.)

#### Arenas

When the player enters an arena, the room is automatically locked, the only way to get out is to defeat all enemies inside. when an enemy is killed, a counter is decremented and will reopen the doors once at 0.

#### Shop

The shop is an interactive object when the player is within range, its implementation is based only on a simple 2D Trigger , when one is within range, triggering the corresponding input will trigger feedback (camera effects, animation, particles ...) and display the shop UI.

{{<zooom src="/lambos-tale/Screenshot_06.PNG">}}

## Critical issues

#### Procedural generation

Procedural generation based on 2D Tiles involves problems which could prove to be very disabling if no solution is not found. Using 2D colliders for each tile, collision bugs can frequently appear at intersections, where the player can get stuck in the tiny space between two tiles. To work around this problem and improve performance, we can use 2D Composite colliders to "merge" several colliders together, but this involves dividing the types of colliders into layers, which is not necessarily complicated, but is an essential phase to be taken into account in the code.

#### Post-Processing

2D rendering in a 3D environment can cause problems on Unity. For characters and enemies, we have chosen to use sprite renderers to support 2D tilemap animations. However, sprite renderers are not meant to be used in 3D rendering, especially on the new scriptable render pipelines.
Using 3D materials on a sprite renderer simply doesn't work, and using 2D materials caused conflicts with the post processing used (especially depth of field).
For this reason we had to create a 2D specific shader, fixing the 3D problems.

{{<zooom src="/lambos-tale/materials.png">}}

<div align="center"><i>3D shader | 2D shader | Custom shader </i></div>
</br>

----

<div align="center"><iframe frameborder="0" src="https://itch.io/embed/760286?linkback=true&amp;bg_color=222222&amp;fg_color=eeeeee&amp;border_color=363636" width="552" height="167"><a href="https://cfaz.itch.io/lambos-tale">Lambo's Tale by cfazilleau</a></iframe></div>

</br>
<div align="center"><img src="/lambos-tale/TeamLambo.png"></img></div>
</br>

{{<center text="Programmers: Julien SOYSOUVANH, Philippe YI, Grégoire PENON, Clément FAZILLEAU">}}
{{<center text="Designers: Max DROULEZ, Adrien BORDES, Grégory RUMEBE, Tony ZHANG ">}}
{{<center text=" Artists: Jade PERDRILLAT, Mélanie L'HUILLIER, Salomé LYSIMAQUE CHAPUIS ">}}

