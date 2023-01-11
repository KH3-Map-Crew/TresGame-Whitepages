# Modding custom maps for KH3 through Unreal Engine


------------------------------------------------------------------------------------------------------------------------------

# Contents
- [Installation](#installation-of-tresgame-and-narkengine)
- [Resources](#resources)
- [TresGame](#tresgame)
	- [NPCs](#npcs)
	- [Enemies](#enemies)
	- [Flowmotion](#flowmotion)
	- [Audio](#audio)
	- [Miscellaneous](#msc)
- [Tres Game Blueprint Library](#tres-game-blueprint-library)
- [TODOs](#todos)
- [Contributing](#contributions)


------------------------------------------------------------------------------------------------------------------------------

## Installation of TresGame and NarkEngine

This proccess is thoroughly documented here:

[Narkon Engine and TresGame Installation](https://github.com/KH3-Modding-Org/OpenKH3Modding/blob/main/uProject%20and%20Engine%20Installation.md#2-github-clone-install---update-with-the-click-of-a-button)

## Useful Resouces
All pawn IDs are listed here: [OpenKh Documentation](https://openkh.dev/kh3/pawns.html)

OG Map references: [Noclip.website](https://noclip.website/)

------------------------------------------------------------------------------------------------------------------------------

# TresGame Actors and Blueprints

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

------------------------------------------------------------------------------------------------------------------------------
# Audio

Audio for Kingdom Hearts III uses proprietary formats. In-engine they use SQEXSEAD_ types to indicate the custom audio formats being used. This applies to both sound and music.

## Custom audio
It is possible to inject custom audio. But it isn't simple.
A guide for this process exists here:

[Audio replacement guide](https://docs.google.com/document/d/1ca5pJjdLSeR-W06YMHIUok0qFl6xJepmOUUkKHDwfu8/edit#)

[Custom audio asset creation guide](https://docs.google.com/document/d/1sPipbu2Bm4009zENsj7x9iSbzcfpe6IdhHint2QNhew/edit)

------------------------------------------------------------------------------------------------------------------------------
# MSC 

## Tres Reactor
Should contain both reaction command prompt visual as well as an event that fires when prompt is pressed.

TODO: Unable to get working consistantly. Requires additional research and documentation.

## Save point
See `/Content/Blueprints/Gimmick/ex/g_ex_SavePoint`

NOTE: Cannot load save made from custom point

TODO: Additional research required for making saves work on custom maps. World configuration is likely required.

------------------------------------------------------------------------------------------------------------------------------
# Tres Game Blueprint Library
A bunch of common game functionality is stored here. From battle states, to in-game cinematics.
	
## Tres Set Special Battle Mode
Toggles the "required" "red command" battles. Not dependant on the existance of enemies.

## Tres Get Friend Manager
Get the class that manages friend NPCs. Required for changing party members.

## UI
Note: Most if not all vitible text in KH3 is in the form of `TresLocText` which can be made through the `Make TresLocText` node.

### Command Menu

#### Tres UI Add Action Command Mode
Non-funcitonal reaction command prompts. Select from an enum `COMMAND_KIND` to specify text displayed in prompt.

It is currently unknown if custom prompts can be added.

#### Tres UI Delete Action Command Mode
Removes an existing reaction command prompt of the kind `COMMAND_KIND`.

### Information

#### Tres Open Information
Given information text, an optional display time, and whether or not the information prompt closes automatically, display an `Information!` prompt on screen.

Closes any existing information UI element before displaying the new one.

#### Tres UI Close Information
Pre-emptively closes an information UI element before it automatically closes.

### Cinematics

#### Tres Start Cinematic Mode
Contains numerous flags for configuring how the cinematic will behave.
EG: Can player move? Will AI continue to act like normal or pause?

#### Tres End Cinematic Mode
Ends the flags triggered by starting cinematic mode.
EG: If control was taken away from the player, it will be returned.

------------------------------------------------------------------------------------------------------------------------------
## TODOs
- Finish basic documentation
- Flesh out Tres Game Blueprint Library doucmentaiton (there's a lot)
- Figure out splines.
- Figure out reactor component for visuals.
- Add accomapnying images detailing specific pieces of functionality where noted.

------------------------------------------------------------------------------------------------------------------------------

## Contributing
If you have any edits or additions you wish to make, you can see the [GitHub project](https://github.com/CpazR/TresGame-Whitepages) and make your contributions!

Just be aware all changes will be vetted before being added through the pull request process.