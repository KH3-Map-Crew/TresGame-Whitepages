---
title: TresGame Whitepages - Tres Level Script Actor
---

# Tres Level Script Actor

[Back to index](index.md)

## Overview

There is a lot of map specific funcitonality what is configured in the level blueprint actor.

This is a blueprint dedicated to a given scene in unreal engine. Typically accessed as so:

![open level blueprint](images/2023-12-07%2017_07_21-.png)

Using Nark Engine and TresGame, it should default a new level to use the `TresLevelScriptActor`.
You can verify this in the class settings in the `Parent Class` dropdown.

![parent class in class settings](images/2023-12-07%2017_08_05-TresGame%20-%20Unreal%20Editor.png)

This will open up a lot of map-specific functionality.

## Accessing from other blueprints

If you want to call this functionality, it would be as simple as calling a `Get All Actors of Class` and pass in `TresLevelScriptActor` as the class and grab the first result.

![get all actors of class example](image/../images/2023-12-07%2017_19_55-TresGame%20-%20Unreal%20Editor.png)

From there, you should be able to call any public function or event you have access to.

## Functions

In the level blueprint, you will find that there are a lot of functions and events you can override:

### TODO: Remove image and just use a properly documented/indexed list
![a lot of functions to override](images/2023-12-07%2017_08_29-TresGame%20-%20Unreal%20Editor.png)

### TODO: A lot to document here. Including tutorial and asset loading stuff.

### Tres Set Pause Menu Type

Select an enum value of type `ETresPauseMenuType`.

- Normal
- Event Skip
- Event Skip But Disallow
- Mini Game
- No Retry Mini Game
- Tutorial

## Events

These can be overridden in the level blueprint to hijack custom funcitonality into certain scenarios.

### On Event Skip

When the skip option is selected in the pause menu when enabled (See `TresSetPauseMenuType`), this event will be called.

### On Camera Manager Initialization
### On Camera Initialization Completed
### On Generic Event
### On Quit Mini Game
### On Tutorial Skip
### On Wipe Out
### On Wipe Out Gummi
### Receive Tres Enemy Killed
### Receive Tres Friend Take Damage
### Receive Tres Player Take Damage
### Receive Tres Ride Vehicle
### Receive Tres Taking Photo Finish (???)
