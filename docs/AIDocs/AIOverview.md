---
title: TresGame Whitepages - AI
---



[Back to index](../index.md)

[Back to AI](../AI.md)
# AI Node Overview

>[!CAUTION]
<text style="color: red">I highly highly recommend you make a few blueprints before tackling AI.</text> Knowing basic programming logic is extremely helpful, and most likely you will end up creating blueprints to interact with your AI if you need anything new beyond what is made available by Tres. This guide assumes you understand basics such as actors vs classes, pawns, loops, components, anim notifies, and variable types such as int/float/bool/enum.

This first part covers the basics of AI in ue4/KH3. Most of it is kh3 centric, but some parts are universal to UE.

* [<ins>Blackboard (BB)</ins>](Blackboards.md): Container for variables for AI. Variables are called blackboard keys. Each actor can have its own blackboard and own variables, but you can sync specific keys across blackboards if you’d like.
* [<ins>Behavior Tree (BT)</ins>](BehaviorTree.md): the core of AI in kh3, makes decisions top to bottom then left to right. This is how you control an AI’s decisions.  
* [<ins>States</ins>](States.md): KH3 uses a hybrid state/Behavior Tree system. States are set for each character, such as running, jumping, attacking, etc. Each state has its own class, either C++, BP, or both. The states are generally c++, but you can extend them using blueprints, allowing you to create your own states. Behavior trees allow you to automatically control the state machine. The behavior tree makes decisions, while the state carries out the action. If you look in the extracted files, you will see many states alongside behavior trees. For example if you look in blueprints\>npc\>n\_ex002\>BT, you will see n\_ex002\_Attack6\_Tornado. This is a blueprint of the Goofy Tornado state. Goofy’s behavior tree determines when to use Tornado, but carrying out tornado, such as movement and other effects are inside the state.
* [<ins>Blueprints</ins>](AIBlueprints.md): There are a few ways to interact with AI using functions and nodes through blueprints. See blueprint nodes for more information.  
* [<ins>Environmental Query System (EQS)</ins>](EQS.md): UE system to scan the environment for the best potential result. Each query can be setup to weigh potential candidates against each other using tests. For a very simple example, you want an enemy to scan actors to find the player to set as its target. KH3 uses this. Then, you want it to scan the environment for suitable locations to run around to while waiting to attack. EQS passes the best result after those tests and places it in a blackboard key of your choosing. (You can also run an EQS through a bp if you need)  
* <ins>Navmesh</ins>: While I don’t plan on going in depth on navmesh in this guide due to existing in other guides, navmesh is how AI determine to move around on the ground. You can generate them in engine on your maps.   
* <ins>Mercuna</ins>: Flying/swimming characters use Mercuna for navigation, which is not able to be used in engine. If you want to make a flying character, you must add a mercuna navigation comp to the pawn.  
* <ins>Controller</ins>: AI pawns are possessed by an ai controller. Other than for making npcs swimming, I have never needed to change or modify a controller. You should leave this as default to whatever class of pawn you use.

# Specific Node Documentation

-[Blackboard](Blackboards.md)  
-[Behavior Tree](BehaviorTree.md)  
-[States](States.md)  
-[Blueprint Nodes](AIBlueprints.md)  
-[Environmental Query System](EQS.md)
