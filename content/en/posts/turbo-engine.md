---
title: "Turbo Engine"
date: 2019-06-20
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: []
description: a 3D game engine...
---
## TurboEngine

is the second-year's end project that I realized in a team of 4.

The goal of this one was to make a game engine with an editor and use them to create a puzzle game.

The technologies used were free for us to choose.

{{< youtube foICXHojFiI >}}

## Engine

The engine has been designed to allow the user to create 3D video-games in an intuitive and fast way.

It uses a PBR (Physically Based Rendering) pipeline including post-process effects, allows the use of realistic physics via the NVIDIA PhysX 3.4 library, sound via the FMOD library, and adding features via C++ scripts .

The scenes are composed of entities related to each other by parent-child relationships.
Every entity can have components attached to them to give it an appearance, physics, data or behavior.

{{< zooom src="/turbo-engine/viewports.gif" >}}

## The Editor

The editor we created works with a project system, which allows us to pair it with versioning software like Git for use on a large project.

Several panels are available for ergonomic and fast use. These panels are:

- SceneTree

The SceneTree is a hierarchical view of the current scene. You can add / remove entities, reparent them, or even rename them to organize your project.

- Properties

The list of components attached to the selected entity. The information can be updated in real time to allow the user to view or try values ​​during runtime.

- Viewports

The viewport is the panel by which one can move in the scene in free camera. Gizmos allow the user to move, rotate, or change the scale of an object. You can create up to 4 to have 4 different views of the scene.

- Game

The panel game is the panel in which the game runs in play mode. It allows to see with the point of view of the main camera of the game.

- Logger

The logger displays all the logs / warnings / errors of the engine, game and hot-reload.

- File explorer

A file explorer allowing you to see the resources of the project and to access them quickly.

- Sound mixer

Used to mix the different audio channels of the game

- Sound list

Simple access to pre-listen to project audio files

- Material editor

To create and edit materials

- Physic settings

To manage the physical parameters of the project (fixed time, physic channels ...)

{{< zooom src="/turbo-engine/physic.gif" >}}

*What have I done...*

### Components

There are 4 categories of accessible components in the properties window:

- The "Data" components

Do not contain logic. They only serve to store data (for example, Transform)

- The "Render" components

define everything that will be visual to the entity (mesh renderer, light ...)

- The "Physic" components

Indicates the physics of the object (Collider, Rigidbody ...)

- The components "Behavior"

Which are used to give a behavior to the object.

{{< zooom src="/turbo-engine/scripts.gif" >}}

Some basic components exist in the engine, but a complete reflection system allows the user to create its own components in C++ and compile and reload those scripts directly from the editor.

{{< zooom src="/turbo-engine/reflection.gif" >}}

*and compilation from the editor*

------

<div align="center">A project by Gregoire PENON, Basile COMBET, Julien SOYSOUVANH and Clément FAZILLEAU</div>