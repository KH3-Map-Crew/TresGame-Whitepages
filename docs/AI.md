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

-   Choose the enemy you will be using as your base
    -   All enemies fall under `Blueprints/Enemies/e_exNNN`
-   Copy the existing pawn and move it to where you build your package
    -   EG: `my_tres_project/PackedBuilds/Enemy/e_exNNN_myVariant`
    -   You don't want to open and modify the pawn in the editor, this will break many of the references.
-   Open the pawn in UAssetGUI or your editor of choice.
-   Replace all instances of `e_exNNN_Pawn` and it's variants with your new custom name
    -   EG: `e_exNNN_Pawn` -> `e_exNNN_myVariant_Pawn`
-   Click `File - > Save As` and save the pawn using your new name.

## TODO: Finish documenting this process
