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