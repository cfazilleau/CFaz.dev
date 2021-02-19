---
title: "Slide Slide Little Penguin!"
date: 2019-05-19
author: "Clément Fazilleau"
draft: false
categories: [ Project ]
tags: [ Game, Mobile, Unity ]
description: Un petit jeu mobile conçu comme un projet mathématique...
---

## Slide Slide Little Pingouin

est un petit jeu mobile créé en tant que projet mathématique. Le but de ce projet était de créer un "clone" de *Tiny Wings* ou *Dune* et ainsi de générer de manière procédurale un terrain 2D infini et de développer la physique s’appliquant à celui-ci.
L'objectif secondaire de ce projet était de créer un jeu mobile optimisé et stable.

{{< youtube lp4QMA8zNrQ >}}

*L'enregistrement depuis mon téléphone n'a pas été d'aussi bonne qualité que prévu.*

------------

## Le jeu

Le principal problème de ce type de jeu est de créer un terrain infini de manière procédurale et en temps réel sans affecter les performances.
Pour résoudre ce problème, nous devons organiser notre terrain en différentes portions de courbes, alignées les unes sur les autres, afin de créer des "collines" aléatoires sur lesquelles notre personnage glissera pour aller aussi loin que possible dans un court laps de temps.

## Affichage

le rendu du terrain est effectué en post-process, en calculant les points de la courbe par rapport à l'écran, ce faisant, le rendu de 5 ou 5 000 courbes ne présentera aucune différence de performances. De plus, les parties de courbes en dehors de l'écran ne seront jamais rendues.

Ce type de rendu est intéressant car il évite de générer des meshs ou des splines en temps réel, ce qui aurait coûté beaucoup plus cher en performances, et il nous permet également de créer très simplement une physique vraiment personnalisée.

{{< zooom src = "/slide-slide-little-penguin/editor.png" >}}

## La physique

La physique créée pour ce jeu est totalement personnalisée et optimisée, ce qui a permis d’éviter le système de physique et de collisions d'unity, qui aurait été beaucoup trop exagéré pour le type de jeu souhaité, le terrain étant généré de manière procédurale.

La physique fonctionne en utilisant uniquement la position et la vitesse du joueur, ainsi que la position et la tangente à la courbe située directement en dessous. De cette façon, la physique n'affectera pas le reste du terrain, ce qui serait inutile sachant que le joueur est la seule entité dynamique du jeu.

---------------

<div align = "center"> Un projet par Julien SOYSOUVANH et Clément FAZILLEAU </div>