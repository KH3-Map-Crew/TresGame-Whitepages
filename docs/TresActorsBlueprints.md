---
title: TresGame Whitepages - Tres Game Actors and Blueprints
---

# Tres Game Actors and Blueprints

[Back to index](index.md)

## NPCs

For AI to work, a Nav Mesh Bounds Volume needs to be added.

### Party members (Set Friend)

Given the ["Friend manager"](#tres-get-friend-manager) and a pawn ID (See the OpenKh docuementation) as well as the number slot, spawn a friend into the party.

TODO: insert image with example blue print

### Enemies (Spawn AI From Class)

Dummy pawns need to be used while working in-engine. These are placeholders for calls and references which will be fulfilled in-game

These dummy pawns should be included with the most recent built versions of TresGame.

The referenced node will use these pawns to spawn the referenced AI. (See the OpenKh docuementation for pawn IDs for reference)

## Flowmotion

Flowmotion uses actors in a straightforward manner. Most only requiring to place down a specific actor.

### Wall running (Static mesh)

On any actor with a static mesh component, search for `Enable Wall Run` and enable that flag. This will allow the player to run up the mesh.

TODO: Other flags exist for similar properties, but require additional research and documentation.

### Pole (Tres Pole actor)

Be mindful of nested compoment placement as some might not have zeroed relative coordinates

### Stepping stone (Tres Hop actor)

Be mindful of nested compoment placement as some might not have zeroed relative coordinates

### Rail (Tres Rail Slide actor)

TODO: Requires more research for standardized approach. For now, try looking existing maps for reference.
