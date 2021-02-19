---
title: "Don't Break The Sausage"
date: 2019-09-16T12:47:45+02:00
author: "Clément Fazilleau"
draft: false
categories: [ Project ]
tags: [ Mobile, Unity, Jam ]
description: A mobile game made in one week.
---

## Don't Break The Sausage

is a game I created for the "game week" (a one week game jam) in my school.

I was in a team composed of 2 Programmers, 1 Game Designer, 3 Game Artists and also 2 Sound Designers.

{{< youtube jDkyII-2-qI >}}

my main challenge on this project was the physics of the sausage and the bread.

I began by making a script that creates gameobjects with 2D colliders, rigidbodies, and hinge joints attached to each others.
I then generated a Bezier spline going through all thoses gameObjects. I then used this curve to create a 2D mesh for the sausage. this way, it looks nice and smooth even if the sausage is twisted.

{{< zooom src="/dont-break-the-sausage/dev.png" >}}

this technique I used is working well, but there is also other options, like using a post-processing shader instead of generating a mesh, but for mobile platforms, post processing support depends a lot of the phone and I chose stability over performances here.

{{< zooom src="/dont-break-the-sausage/sidebyside.png" >}}

Don't break the sausage was awarded the Originality prize at the end of the week, and has been offered the opportunity to be published by webedia games.

{{< image src = "/dont-break-the-sausage/award.png" >}}
