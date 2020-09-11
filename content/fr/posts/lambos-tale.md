---
title: "Lambo's Tale"
date: 2020-06-02
author: "Clément Fazilleau"
draft: false
categories: [ "Project" ]
tags: [ game ]
description: Un metroidvania 2D créé pour ma troisième année à ISART.
---

## Introduction

Lambo's Tale est un jeu de plateformes en 2D implémentant des mécaniques Metroidvania. 
Il a été créé en tant que projet de fin de troisième année et dont la production a durée un peu plus de quatre semaines en compagnie de 3 merveilleux programmeurs, 4 formidables designers et 3 talentueuses artistes (tous les noms sont cités à la fin de l'article).

La spécificité plutôt inattendue de ce projet est le fait qu'il ait été réalisé entièrement à distance, dû au confinement lié au Covid-19. Malgré ce désagrément, une bonne communication interne au groupe ainsi que des efforts fournis par chacuns des membres de l'équipe ont permis de mener à bien ce projet.

{{<youtube 6GjfYDQagJo>}}

Le jeu nous raconte l'histoire de Lambo, un petit agneau qui part combattre des meutes de loups afin de venger sa soeur, Lambette.
Il devra traverser divers niveaux très variés et récoltera des oeufs en or qui lui permettront d'acheter des nouvelles capacités afin d'augmenter ses compétences (santé, résistance, attaque).
Dans chaque niveau se situe aussi une arène, appelée "Wolf's Den" qui nous permettra de gagner de nouvelles attaques en combattant tous les ennemis qui s'y trouvent.

A la fin d'un niveau, on trouvera un livre qui nous permettra de passer au suivant. Il y a trois niveaux en tout, les deux premiers étant générés de manière procédurale.

{{<zooom src="/lambos-tale/Screenshot_04.PNG">}}

## Spécificités techniques

Le jeu a été développé sur Unity 2019.3.7f1, ce qui nous a permis d'utiliser des fonctionnalités spécifiques (notamment à la 2D), telles que:

- **Universal Render Pipeline** qui nous a permis de créer des shaders en utilisant le Shader Graph, qui s'est trouvé plutôt utile pour créer ce type de rendu mixte entre 2D et 3D.
- **2D Collisions**, bien que le rendu soit en 3D, les collisions sont effectuées en 2D, afin de supporter les tilemaps, et d'obtenir de meilleures performances.
- **Tilemaps 2D / Grid** qui sont utilisés par la génération procédurale afin de créer les niveaux.
- **Rule Tiles** qui sont utilisées afin de connecter les tiles entre elles et obtenir cet effet de terrain lisse. elles nous permettent aussi de générer des tiles en "3D".
- **Platform effector 2D** utilisés pour les *one-way platforms*
- **PSD importer** qui allègent la charge de travail des artistes et nous permettent d'implémenter rapidement textures et sprites.
- **Scriptable objects** qui sont utilisés pour stocker des données sur les skills, capacités, items de la boutique, etc...

Le Scripting en C# de Unity nous a permis d'iterer et de tester nos fonctionnalités rapidement et de manière efficace, ce qui est un point non négligeable compte tenu du scope du projet. L'utilisation de ce moteur nous a aussi permis d'avoir accès à différents packages:

- **Cinemachine** a été utilisé pour tous les effets de caméra, c'est un outil accessible qui nous a permis de créer une caméra intuitive et correspondant parfaitement à ce type de platformer dynamique.

- **Animancer** est un plugin qui nous a permis de contrôler de maniere tres precise les animations de tous les personnages du jeu, le système de combat etant extremement precis, l'utilisation des animations d'unity aurait été chaotique à mettre en place, et aurait eu un trop gros impact sur les performances.

- **Input System**, ce nouveau système de gestion des inputs est destiné à remplacer l'actuel Input Manager d'unity. nous avons souhaité l'utiliser afin de nous former un peu plus à cet outil. Les inputs de base auraient aussi demande une base de code non négligeable, ou des bindings manuels qui auraient ete nefaste pour l'architecture de notre projet.

{{<zooom src="/lambos-tale/Screenshot_03.PNG">}}

## Fonctionnalités

#### Player Controller

Le controller du joueur nécessitait les features suivantes:
- mouvement simple
- saut
- wall-jump
- wall-slide
- dash (dans le style de "Celeste")

Afin d'avoir un ressenti agréable et permettre aux designers de "tweak" facilement les différents paramètres, les choix de technologies suivantes ont été faits:
Le Player Controller utilise un simple Rigidbody 2D ainsi qu'un Box Collider 2D, pour pouvoir bénéficier de la physique de Unity et de sa résolution de collisions, cependant, la vélocité du joueur est entièrement calculée dans ce script pour garder un contrôle total sur tous les mouvements.

Le controller bénéficie aussi de:
- Coyote time, permettant au joueur de sauter quelques millisecondes après être tombé d'une plateforme. 
- Jump buffering, permettant au joueur d'effectuer facilement des "frame-perfect jumps"
- Snapping, lorsque le joueur heurte un coin de mur, le jeu essaiera de modifier la trajectoire du joueur afin d'éviter le mur.

Ces trois features sont présentes dans le jeu "Céleste", qui a été une grande source d'inspiration pour notre projet. vous pouvez trouver plus d'informations sur ces features [ici](https://twitter.com/MattThorson/status/1238338574220546049).

Les différents états du controller étaient gérés via un pattern de HFSM (Hierarchical Finite State Machine), utilisant un système de transitions universel, dans le but de permettre d'ajouter facilement des nouveaux etats.
cependant, la faiblesse de ce système est la cause de potentiels bugs de transitions d'états invalides, qui auraient été plus facilement évités ou réparés en utilisant un autre design pattern.

{{<zooom src="/lambos-tale/Screenshot_05.PNG">}}

#### Input buffer

le système d'auto-combo pour le combat a nécessité l'utilisation d'un Input buffer afin de permettre au joueur de déclencher et annuler des animations d'attaque de manière fluide.
l'input buffer enregistre les dernières X actions en gardant en mémoire le timestamp de son déclenchement le controller peut alors "consommer" les inputs et choisir de les valider ou non, dépendamment de son état.

le buffer utilisé est un buffer circulaire, afin de réduire au maximum les allocations au runtime et garder toujours une taille de mémoire fixe.

#### Génération procédurale

Chaque niveau est généré de manière procédurale (via tile grids 2D) pour etre sur que chaques niveaux seront différents, cependant, il est possible pour les Game Designers de créer des portions de niveaux qui ne seront pas affectés par la génération procédurale. Pour cette raison, le générateur doit utiliser à la fois de l'aléatoire et des algorithme de pathfinding, implémenté ici via un simple algorithme A* (A star). Cet algorithme permettra de joindre les différentes contraintes spécifiées, et un système de budget permettra de faire un tracé plus ou moins linéaire.
lorsque le path est construit, des salles aléatoires y sont assignées selon des contraintes sur leurs ouvertures (droite/gauche/haut/bas). pour y ajouter encore plus de random, chaque design de salle contient des éléments aléatoires (ennemis/obstacles/bonus...) contrôlés par des probabilités réglées par les game designers.

{{<zooom src="/lambos-tale/Screenshot_10.png">}}

#### Système de combat

lorsque le joueur attaque ou utilise une capacité, le character transitionne vers l'état correspondant, en annulant tout état de non combat pour jouer l’animation correspondante et déclencher les événements spécifiques à beaucoup de jeux de combat:

- Startup (la plupart des animations peuvent etre annulees dans cet état)
- Active (application de l'attaque,  ne peut pas être annulé)
- Recovery (le character ne peut pas bouger)
- End (le contrôle est repris)

Ces événements sont utilisés pour contrôler le comportement des attaques et leurs hitboxes. il est particulièrement important dans notre cas puisque l'input buffer permet d'enchainer les attaques (auto combo) ce qui implique que le framedata soit le plus précis possible.
Etant donné la diversité des attaques et capacités, les animations doivent être facilement modifiables et disposer de suffisamment de paramètres différents.

#### Items

Différents items peuvent être ramassés par le joueur (bonus de santé, clés, monnaie, compétences), et certains items doivent pouvoir être ajoutés durant la production. C'est la raison pour laquelle l'architecture du code devraient être très flexible sur ce point.
tous les "pickables" héritent donc d'une classe implémentant le comportement de "Pick". on distingue plusieurs sortes de pickables, par exemple, certains sont fait pour être stockés (comme des capacités par exemple) et d'autres devront être instantanément consommés (santé).
Dans un seul niveau, il pourra y avoir en même temps des centaines de pickables, c'est pourquoi un système de pooling a été implémenté pour les items.

{{<zooom src="/lambos-tale/Screenshot_02.PNG">}}

#### Plateformes

Le level-design contiendra des "one-way platforms", des plateformes au travers desquelles le joueur peut passer, mais seulement dans un sens (du bas vers le haut). Le component "Platform effector 2D" de Unity a été créé justement pour ce comportement. ces plateformes ont également des réglages physique spécifiques afin de d'éviter des comportements inattendus (wall jump, slide...)

#### Arènes

Lorsque le joueur entre dans une arène, la salle est automatiquement verrouillée, le seul moyen d'en sortir est de vaincre tous les ennemis à l'intérieur. lorsqu'un ennemi est tué, un compteur est décrémenté et permettra de rouvrir les portes une fois a 0.

#### Boutique

La boutique est un objet interactible lorsque le joueur est a portee, son implémentation ne repose que sur un simple 2D Trigger, lorsqu'on est un à portée, déclencher l'input correspondant permettra de déclencher des feedbacks (effets de caméra, animation, particules...) et d'afficher l'UI du shop.

{{<zooom src="/lambos-tale/Screenshot_06.PNG">}}

## Problématiques critiques

#### Génération procédurale

La génération procédurale basée sur des Tiles 2D implique des problèmes qui pourront s'avérer très handicapant si aucune solution n'est trouvée. en utilisant des colliders 2D pour chaque tiles, des bugs de collisions peuvent apparaître fréquemment aux intersections, où le joueur peut se coincer dans l'espace infime entre deux tiles. Pour contourner ce problème et améliorer les performances, nous pouvons utiliser des Composite colliders 2D afin de "merge" plusieurs colliders entre eux, Mais cela implique de diviser les types de colliders dans des layers, qui n'est pas forcément compliqué, mais est une phase essentielle à prendre en compte dans le code. 

#### Post-Processing

Un rendu 2D dans un environnement 3D peut causer des problèmes sur Unity. Pour les personnages et ennemis, nous avons fait le choix d'utiliser des sprite renderers afin de supporter des animations 2D en tilemaps. Cependant, les sprite renderers ne sont pas supposés être utilisés dans un rendu 3D, et d'autant plus sur les nouvelles render pipelines.
L'utilisation de matériaux 3D sur un sprite renderer ne fonctionnent simplement pas, et l'utilisation de matériaux 2D causaient des conflits avec le post processing utilisé (notamment depth of field).
Pour cette raison nous avons du créer un shader spécifique à la 2D, réglant les problèmes de la 3D.

{{<zooom src="/lambos-tale/materials.png">}}

<div align="center"><i>Shader 3D | Shader 2D | Shader custom</i></div>
</br>

----

</br>
<div align="center"><img src="/lambos-tale/TeamLambo.png"></img></div>
</br>

{{<center text="Programmeurs: Julien SOYSOUVANH, Philippe YI, Grégoire PENON, Clément FAZILLEAU">}}
{{<center text="Designers: Max DROULEZ, Adrien BORDES, Grégory RUMEBE, Tony ZHANG">}}
{{<center text="Artistes: Jade PERDRILLAT, Mélanie LHUILLIER, Salomé LYSIMAQUE CHAPUIS">}}
