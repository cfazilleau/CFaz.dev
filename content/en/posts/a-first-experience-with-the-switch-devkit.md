---
title: "A first experience with the switch devkit"
date: 2020-03-15
author: "Clément Fazilleau"
draft: false
tags: [ game ]
description: A Research and Development project on the switch devkit.
---

During my third year at ISART, I was given the opportunity to make a 2 week project using the Nintendo Switch Devkit. This is not an opportunity frequently given to students so my friend Julien and myself grabbed this opprtunity. Here is what we learned:

> This post is a summary of the paper we had to write about our journey with the switch devkit. As you would expect, a lot of what we learned was strictly confidential and under the protection of a NDA (Non-Disclosure Agreement) from Nintendo. If you are reading this trying to find private information about the devkit and softwares used, you won't find anything on this page. This being said, let's get into it.

You can also read the article about [Poshon, the game we created during this project.](/posts/poshon)

## Why this R&D choice

We chose this research and development project in the first place for the opportunity given to us.

Working on Nintendo Switch is a privilege that we are not sure we will have in the future and it was an opportunity to see and use professional tools from licensed consoles.

It was also a personal challenge since we had the objective of developing a complete game, during the only two weeks of the project.

The choice of Unity as Engine was made because we wanted discovered at the same time the input system packages as well as the Universal Render Pipeline (but the version of unity being too old, we had to fall back on the Lightweight Render Pipeline). This engine also allowed us to carry out fast and simple prototyping.

<img style="height:100px; margin:auto;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Unity_Technologies_logo.svg/1280px-Unity_Technologies_logo.svg.png"></img>

## Our Objectives

The objective we set for this project was to develop a complete game on unity 2019 by learning and using the following functionalities:

- The joycons.

These are the controllers of the switch. With the possibility of connecting up to eight on the same machine, we focused on local multiplayer gameplay, supporting a maximum of eight players. The controllers also have gyroscopes, a feature that we used in our game.

- The Lightweight render pipeline.

This is a preview package that appeared with the 2019 version.1 of unity, it was created to obtain more performance than the classic rendering pipeline on platforms such as mobiles or machines with a weak configuration. We made this choice based on the performance offered by the console, close to that of a high-end smartphone.

- The "Input System" package.

Intended to replace the current input manager of the engine, we used this tool, although it is still in preview, to know its specificities and its weaknesses.

<img style="height:150px; margin:auto;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/Nintendo_Switch_Logo.svg/800px-Nintendo_Switch_Logo.svg.png"></img>

## Hardware

> I chose to keep this part private as it was containing mostly confidential informations from Nintendo under the protection of a NDA (Non-Disclosure Agreement).

## Devkit and SDK

> I chose to keep this part private as it was containing mostly confidential informations from Nintendo under the protection of a NDA (Non-Disclosure Agreement).

## Performances and Debugging

> I chose to keep this part private as it was containing mostly confidential informations from Nintendo under the protection of a NDA (Non-Disclosure Agreement).

## Joycons

> I chose to keep this part private as it was containing mostly confidential informations from Nintendo under the protection of a NDA (Non-Disclosure Agreement).

## Lightweight Render Pipeline

The LightWeight Render Pipeline (or LWRP) is a Unity package using the new "Scriptable Render Pipelines" (or SRP) and is optimized for low performance machines such as mobiles.

It is from this observation that we chose to use it for the switch, In addition, its opposite, the High Definition Render Pipeline (or HDRP) was too powerful and demanding in resources, and it would have been useless to choose such a big feature, and it would even have been risky to make this choice and end up in the middle of the project having to re-target the project on the LWRP, and having to recreate all the materials, shaders, and other resources specific to rendering.

LWRP being basic, we still used a large amount of its features, such as anti-aliasing, shadows, dynamic materials, shaders (created from the new "Shader Graph") or post processing effects such as "Vignette", "Bloom", and "Color Correction".

{{< zooom src="/a-first-experience-with-the-switch-devkit/LWRPSettings.png" >}}

## Input System

The input system is a package available since Unity 2019.1, in version 1.0.0-preview-4 during our project. It was risky to use it, given its instability. We however used it at first to train on it, but also because its implementation of the switch controllers was very accessible and cross-platform, allowing us to test our game from our PCs, using classic Xinput controllers.

The aim of this package is to standardize the inputs as much as possible, via Control Schemes (binding schemes to a specific "device") or Player Inputs (component used to forward inputs from a device to a gameobject, in this way, an object A will only receive the inputs from a controller A and an object B will only receive the inputs from a controller B). This package also allows direct support for multiple devices and custom devices.

The main problem encountered in the Input System is the instability of this package. It works perfectly in a single player game, but is more complex in multiplayer, for example, controlling the GUI from several controllers, or when adding players. The code of this package was also relatively poorly documented, and some methods are not yet implemented.

{{< zooom src="/a-first-experience-with-the-switch-devkit/InputActions.png" >}}

## Other Features

> I chose to keep this part private as it was containing mostly confidential informations from Nintendo under the protection of a NDA (Non-Disclosure Agreement).

## Conclusion

We learned a lot thanks to this project, and have discovered big constraints, which were finally easily overcome thanks to Unity (and its Input System)

It was very pleasant working on Unity, for its fast compilation time, its low build time, the simplicity of its architecture, and thanks to the packages used. The same game using Unreal engine would ~~probably~~ have required (a lot) more time.

The resources used were found on the internet or the asset store, or modeled or drawn by us, despite the absence of Game Designers, Artists, or Sound Designers, the result is still fun and the game is widely playable.

{{< zooom src="/a-first-experience-with-the-switch-devkit/Poshon.png" >}}
