---
title: TresGame Whitepages - AI
---



[Back to index](index.md)

[Back to AI](./AI.md)
# AI Overview
This first part covers the basics of AI in ue4/KH3. Most of it is kh3 centric, but some parts are universal to UE. $\color{red}{\text{I highly highly recommend you make a few blueprints before tackling AI}}$, knowing basic programming logic is extremely helpful, and most likely you will end up creating blueprints to interact with your AI if you need anything new beyond what is made available by Tres. This guide assumes you understand basics such as actors vs classes, pawns, loops, components, anim notifies, and variable types such as int/float/bool/enum.

* <ins>Behavior Tree (BT)</ins>: the core of AI in kh3, makes decisions top to bottom then left to right. This is how you control an AI’s decisions.  
* <ins>Blackboard (BB)</ins>: Container for variables for AI. Variables are called blackboard keys. Each actor can have its own blackboard and own variables, but you can sync specific keys across blackboards if you’d like.  
* <ins>Environmental Query System (EQS)</ins>: UE system to scan the environment for the best potential result. Each query can be setup to weigh potential candidates against each other using tests. For a very simple example, you want an enemy to scan actors to find the player to set as its target. KH3 uses this. Then, you want it to scan the environment for suitable locations to run around to while waiting to attack. EQS passes the best result after those tests and places it in a blackboard key of your choosing. (You can also run an EQS through a bp if you need)  
* <ins>States</ins>: KH3 uses a hybrid state/Behavior Tree system. States are set for each character, such as running, jumping, attacking, etc. Each state has its own class, either C++, BP, or both. The states are generally c++, but you can extend them using blueprints, allowing you to create your own states. Behavior trees allow you to automatically control the state machine. The behavior tree makes decisions, while the state carries out the action. If you look in the extracted files, you will see many states alongside behavior trees. For example if you look in blueprints\>npc\>n\_ex002\>BT, you will see n\_ex002\_Attack6\_Tornado. This is a blueprint of the Goofy Tornado state. Goofy’s behavior tree determines when to use Tornado, but carrying out tornado, such as movement and other effects are inside the state.  
* <ins>Navmesh</ins>: While I don’t plan on going in depth on navmesh in this guide due to existing in other guides, navmesh is how AI determine to move around on the ground. You can generate them in engine on your maps.   
* <ins>Mercuna</ins>: Flying/swimming characters use Mercuna for navigation, which is not able to be used in engine. If you want to make a flying character, you must add a mercuna obstacle comp to the pawn.  
* <ins>Controller</ins>: AI pawns are possessed by an ai controller. Other than for making npcs swimming, I have never needed to change or modify a controller. You should leave this as default to whatever class of pawn you use.

Blackboards:

# Required tools

-   KHIII compatible Unreal Editor
-   Some sort of asset cooked UE viewer / editor
    -   UAssetGUI
    -   SOD2Editor
-   Patience...

# Required assets

Before you can modify any NPC AI, you need to import or dummy relavent files.

_IMPORTANT_: Remember that when copying files, the file structure in your project needs to match the structure in-game. With the only change being `game` will be `content` in your project.

## Game/AI

-   [Node Documentation](./AI_Home.md)

All the contents in the following folders.

`AI/BehaviorTree/Blackboards`

`AI/EQS`

## Game/Blueprints/Enemy

### TODO: Some of these files are known to crash the editor. Document which files do this and how to create dummy files.

`All`

`Common`

`Any other relavent enemies you plan on modifying`

---

# Creating enemy variants

Currently, the easiet method of custom AI is using existing enemies as a base.

## Duplicating Pawns

-   Choose the enemy you will be using as your base
    -   All enemies fall under `Blueprints/Enemies/e_exNNN`
-   Copy the existing pawn and move it to where you build your package
    -   EG: `my_tres_project/PackedBuilds/Enemy/e_exNNN_myVariant`
    -   You don't want to open and modify the pawn in the editor, this will break many of the references.
-   Open the pawn in UAssetGUI or your editor of choice.
-   Replace all instances of `e_exNNN_Pawn` and it's variants with your new custom name
    -   EG: `e_exNNN_Pawn` -> `e_exNNN_myVariant_Pawn`
-   Click `File - > Save As` and save the pawn using your new name.

## Duplicating EQS


## Duplicating Behavior Trees

Behavior trees can either be modified through an asset editor such as UAssetGUI or SOD2.

It can also be brought into NarkEngine and modified, ***however,*** this will break a lot of references and parts of the behavior tree might require some reconstruction.

This will be covering importing into Unreal engine.

### Importing into unreal

-   Choose the blueprint of the enemy you'd like to bring into UE
    -   Copy it into your project directory
-   Open your project in unreal engine
    -   This is assuming your project doesn't crash
-   Duplicate it in Unreal (Shortcut is `Ctrl + W`) and rename it to something appropriate for your project

### Fixing the behavior tree

This is where the patience comes into play...

Many things will break that will require you compare both the original asset from the game and the recooked-asset from your project.

The blackboard is the first to check when importing a behavior tree.

Use an asset editor to identify and verify these different cases.

For example:

![Incorrect blackboard](images/2023-11-12%2011_34_39-TresGame%20-%20Unreal%20Editor.png)

Should be using `BlackboardPlanBase`:

![Corrected blackboard](images/2023-11-12%2011_34_23-TresGame%20-%20Unreal%20Editor.png)

Once this is fixed, you should also make sure that any instances of `Blackboard<Type>ValueModifier` are using the correct blackbord values.


For example:

![Incorrect blackboard values](images/2023-11-12%2012_01_34-TresGame%20-%20Unreal%20Editor.png)

Should be using inherited values from `BlackboardPlanBase` denoted with the naming prefix `P_`

![Correct blackboard values](images/2023-11-12%2012_01_08-TresGame%20-%20Unreal%20Editor.png)

Also, there will be cases where service or decorators might not be imported at all or imported incorrectly.

For example:

![missing services](images/2023-11-12%2011_33_22-TresGame%20-%20Unreal%20Editor.png)

Is missing it's `Update Target` and `BlackboardBase` modifer services. Again, viewing the original behavior tree in an asset editor should verify this.

![re-added services](images/2023-11-12%2011_33_48-TresGame%20-%20Unreal%20Editor.png)


### TODO: Finish documenting this process
