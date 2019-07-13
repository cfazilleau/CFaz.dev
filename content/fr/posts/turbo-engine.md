---
title: "Turbo Engine"
date: 2019-06-06
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: []
description: turbo Engine
---

## TurboEngine

est le projet de fin de deuxième année que nous avons réalisé.

Le but de ce dernier était de réaliser un moteur de jeu avec éditeur et de l’utiliser afin de créer un jeu de puzzle.

Les choix des technologies utilisées dans notre projet étaient libres.

{{< youtube foICXHojFiI >}}

## Le Moteur

Le moteur a été pensé pour permettre à son utilisateur de créer des jeux-vidéo 3D de façon intuitive et rapide.

Il utilise une pipeline de rendu PBR (Physically Based Rendering) incluant des effets post-process, permet l’utilisation de physique réaliste via la librairie NVIDIA PhysX 3.4, le son via la librairie FMOD, et l’ajout de fonctionnalités via des scripts C++.

Les scènes sont composées d'entités rattachées les unes aux autres par des relations parent-enfants.
Chaque entité peut avoir des composants servant à lui attribuer une apparence, de la physique, des données ou des comportements.

{{< zooom src="/turbo-engine/viewports.gif" >}}

## L'Éditeur

L'éditeur que nous avons créé fonctionne avec un système de projet, ce qui nous permet de le coupler à un logiciel de versionning comme Git pour l'utiliser sur un projet de grande ampleur.

Plusieurs panels sont disponibles pour une utilisation ergonomique et rapide. Ces panels sont les suivants:

- SceneTree

Le SceneTree est une vue en hiérarchie de la scène courante. On peut y ajouter / supprimer des entités, les reparenter, ou même les renommer pour organiser son projet.

- Properties

La liste des composants rattachés à l'entité sélectionnée. Les informations peuvent être mises à jour en temps réel afin de permettre à l'utilisateur de visualiser ou essayer des valeurs au runtime.

- Viewports

Le viewport est le panel par lequel on peut se déplacer dans la scène en caméra libre. Les gizmos permettent à l'utilisateur de déplacer, tourner, ou changer le scale d'un objet. On peut en créer jusqu'à 4 afin d'avoir 4 points de vue différents de la scène.

- Game

Le panel game est le panel dans lequel le jeu s'exécute en mode play. Il permet de voir avec le point de vue de la caméra principale du jeu.

- Logger

Le logger affiche tous les logs/warnings/erreurs du moteur, jeu et hot-reload.

- File explorer

Un explorateur de fichiers permettant de voir les ressources du projet et d'y accéder rapidement.

- Sound mixer

Permettant de mixer les différents channels audio du jeu

- Sound list

Un accès simple pour pré-écouter les fichiers audio du projet

- Material editor

Pour créer et éditer des matériaux

- Physic settings

Pour gérer les paramètres physiques du projet (fixed time, physic channels…)

{{< zooom src="/turbo-engine/physic.gif" >}}
*Drame, Clément - 2019*

### Components

Il existe 4 catégories de composants accessibles dans la fenêtre de propriétés:

- Les composants "Data"

Ne contiennent pas de logique. Ils ne servent qu'à stocker des données (par exemple, Transform)

- Les composants "Render"

définissent tout ce qui sera visuel à l'entité (mesh renderer, light...)

- Les composants "Physic"

Indiquent la physique relative à l'objet (Collider, Rigidbody…)

- Les composants "Behavior"

Qui servent à donner un comportement à l’objet.

{{< zooom src="/turbo-engine/types.png" >}}
*Les 4 cavaliers de l'apocalypse*

Certains composants de base existent dans le moteur, mais un imposant système de réflexion permet à l’utilisateur de créer ses propres composants en c++ et de compiler et recharger ces scripts directement depuis l'éditeur.

------

<div align="center">by Gregoire PENON, Basile COMBET, Julien SOYSOUVANH and Clément FAZILLEAU</div>