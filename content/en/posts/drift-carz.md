---
title: "Drift Carz"
date: 2018-12-19
author: "Clément Fazilleau"
draft: false
categories: [ Project ]
tags: [ Multiplayer, Unity ]
description: A multiplayer arcade game...
---

{{< youtube mVXk2ly4Lh4 >}}

## Drift Carz

is a video-game developped as a school project during my second year at ISART Digital.

its main goal was turning a small racing arcade game into a fully multiplayer game, by creating a C++ Networking DLL for unity.

{{< zooom src="/drift-carz/street.png" >}}

our game had to be featuring the following features:

- __custom lobby creation__ where the host can setup the game (number of laps) and start it.
- __synchronized start__ between clients and host.
- synchronized and shared players positions and physics.
- shared informations between clients (cars colors, names).

but we ended up developping optionnal features as well:

- __master server__ used to reference all servers in one place.
- __chat system__ to talk to other players in game or in the lobby.
- __tweakable capacity__ in order to accept up to 30 players in the same game (we locked this number to 30 by ourselves but the code is flexible enough to add a lot more).
- __room naming__
- and much more...

{{< zooom src="/drift-carz/server.png" >}}
---------------

<div align = "center"> A project by Julien SOYSOUVANH and Clément FAZILLEAU </div>