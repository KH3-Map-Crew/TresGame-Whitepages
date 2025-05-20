---
title: Misc. Pawns

parent: Tres Pawns
---

# Miscellaneous Pawns

[//]: # [Back to index](index.md)

## Save point

>[!WARNING]
>This pre-made blueprint in tresgame-built is currently wrong (5-20-25). Components have incorrect default relative locations. See below for making a proper save point.

See `/Content/Blueprints/Gimmick/ex/g_ex_SavePoint`.

Make a new class from the parent "Tres Save Point Actor". Click on the components "My Reactor" and "My Recover". Set the location (those relative locations) to zero completely. Currently, those components have incorrect pre-set relative locations. If you skip this step, you probably won't be able to use your save point in game.


[//]: # NOTE: Cannot load save made from custom point

[//]: # TODO: Additional research required for making saves work on custom maps. World configuration is likely required.
