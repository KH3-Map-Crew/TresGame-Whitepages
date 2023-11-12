---
title: TresGame Whitepages - AI
---

# AI

[Back to index](index.md)

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
