---
title: "Drift Carz"
date: 2018-12-19
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: ["Multiplayer", "Unity"]
description: Un jeu d'arcade multijoueur...
---

{{< youtube mVXk2ly4Lh4 >}}

## Drift Carz

est un jeu vidéo développé comme projet scolaire durant ma deuxième année à ISART Digital.

son objectif principal était de transformer un petit jeu de course en un jeu entièrement multijoueur, en créant une DLL de réseau en C ++ pour l'unité.

{{< zooom src="/drift-carz/street.png" >}}

notre jeu devait présenter les caractéristiques suivantes:

- __Création de lobby personnalisés__ où l'hôte peut configurer le jeu (nombre de tours) et démarrer la partie.
- __départ synchronisé__ entre les clients et l'hôte.
- position et physique des joueurs synchronisées et partagées.
- informations partagées entre clients (couleurs des voitures, noms).

mais nous avons fini par développer des fonctionnalités supplémentaires:

- __master server__ utilisé pour référencer tous les serveurs au même endroit.
- __système de chat__ pour parler à d'autres joueurs dans le jeu ou dans le lobby.
- __capacité modifiable__ afin d’accepter jusqu’à 30 joueurs dans le même jeu (nous avons verrouillé ce nombre à 30 par nous-mêmes mais le code est suffisamment flexible pour en ajouter beaucoup plus).
- __nommage des lobby__
- et beaucoup plus...

{{< zooom src="/drift-carz/server.png" >}}
------------------

<div align = "center"> Un projet par Julien SOYSOUVANH et Clément FAZILLEAU </div>
