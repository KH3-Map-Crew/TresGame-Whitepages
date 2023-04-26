---
title: TresGame Whitepages - Tres Game Blueprint Library
---

# Tres Game Blueprint Library

[Back to index](index.md)

A bunch of common game functionality is stored here. From battle states, to in-game cinematics.

## Tres Set Special Battle Mode

Toggles the "required" "red command" battles. Not dependant on the existance of enemies.

## Tres Get Friend Manager

Get the class that manages friend NPCs. Required for changing party members.

# UI

Note: Most if not all vitible text in KH3 is in the form of `TresLocText` which can be made through the `Make TresLocText` node.

## Command Menu

### Tres UI Add Action Command Mode

Non-funcitonal reaction command prompts. Select from an enum `COMMAND_KIND` to specify text displayed in prompt.

Custom prompts can be added by means of data tables.

TODO: Need to specify the data table that contains this information.

### Tres UI Delete Action Command Mode

Removes an existing reaction command prompt of the kind `COMMAND_KIND`.

## Information

### Tres Open Information

Given information text, an optional display time, and whether or not the information prompt closes automatically, display an `Information!` prompt on screen.

Closes any existing information UI element before displaying the new one.

### Tres UI Close Information

Pre-emptively closes an information UI element before it automatically closes.

## Cinematics

### Tres Start Cinematic Mode

Contains numerous flags for configuring how the cinematic will behave.
EG: Can player move? Will AI continue to act like normal or pause?

### Tres End Cinematic Mode

Ends the flags triggered by starting cinematic mode.
EG: If control was taken away from the player, it will be returned.
