---
title: TresGame Whitepages - Audio
---

# Audio

[Back to index](index.md)

Audio for Kingdom Hearts III uses proprietary formats. In-engine they use SQEXSEAD\_ types to indicate the custom audio formats being used. This applies to both sound and music.

## Custom audio

It is possible to inject custom audio. But it isn't simple.
A guide for this process exists here:

[Audio replacement guide](https://docs.google.com/document/d/1ca5pJjdLSeR-W06YMHIUok0qFl6xJepmOUUkKHDwfu8/edit#)

[Custom audio asset creation guide](https://docs.google.com/document/d/1sPipbu2Bm4009zENsj7x9iSbzcfpe6IdhHint2QNhew/edit)

## General BGM functions

Some of the referenced functions have either `optional fade` and or `all` variants.

### Is Playing BGM

Determines if a referenced track is currently playing. Requires a valid reference to a `SQEXSEADMusic` object.

### Stop BGM

Ends the currently playing BGM. Will restart if resumed.

Also exists with an "Optional Fade" variant, which requires a fade duration (in sec.)

### Suspend BGM

Suspends the currently playing BGM. If resumed, will continue from the time it was suspended.

Also exists with an "Optional Fade" variant, which requires a fade duration (in sec.)

### Resume BGM

Will resume the music where it left off, with a fade in. The fade duration is set in the BGM controller's parameters.

Also exists with an "Optional Fade" variant, which requires a fade duration (in sec.) which will override the BGM controller's.

### Get Musical Time

Given a BGM controller, gets the play time of its currently BGM track. The play time's value ("Musical time") is not in seconds, and does not directly scale with real-time values.

Requires a valid reference to a `SQEXSEADBGMSLot Controller` object.

#### Converting Musical Time values into real-time

Each BGM controller has a (hard-coded?) range of value for the musical time. This range is determined by the duration of the unmodded BGM track that the BGM controller calls:
- BGM track has a loop:
	- Musical time range = -1 to (unmodded BGM track length)/2
- BGM track doesn't have a loop:
	- Musical time range = 0 to (unmodded BGM track length)/2

These values **don't** change even when replacing the original BGM track.

The musical time values are mapped to real-time seconds as follows:
- BGM not playing or stopped --> Musical time = -1
- Non-looping (cutscene/event) BGM is playing --> 1 musical time unit = 2 real-time seconds
- Non-dynamic looped BGM (field/battle/etc.) is playing:
    - Loop hasn't started yet --> Musical time value is scaled from -1 to 0, with 0 = loop start
	- Loop is playing --> 1 musical time unit = 2 real-time seconds
- Dynamic music with looped BGM ("Dive into the Heart (Destati)", "Sunshine Dancer", etc.):
    - Loop hasn't started yet --> Musical time value is scaled from -1 to 0, with 0 = loop start
	- Loop is playing --> 1 musical time unit = every allowed point at which the current BGM can transition into the next "musical" phase
	
### Set Seek Time

Given a BGM controller, sets the play time of its currently BGM track. (Useful for jumping to a different time in a BGM track.)

Requires a valid reference to a `SQEXSEADBGMSLot Controller` object.

The "Seek Time" value is *not* in real-time seconds, but rather in "Musical Time" units. (See "Get Musical Time" node above).

## SQEXSEADBGMSlot Controller

Maintains a BGM slot. Can be accessed through a few methods.

### Get playing BGMSlot Controller

Retrieves the active BGMSlot controller.

### Get BGM Slot Controller

Given the name of a BGMSlot, retreive it's controller.

### Set

Given a controller, set the currently playing track for that BGMSlot.
Requires a valid reference to a `SQEXSEADMusic` object.

#### Switching a BGM controller's track
To force-switch the BGM loaded in a BGM track, chain the following nodes in a blueprint:
1. **Tres Change BGMEnable** ("Enable" must be ticked)
2. **Set** (requires a valid reference to a `SQEXSEADMusic` object)

As long as the current BGM track is playing, the new one will then start.

### Create BGMSlot

Self-explanatory. Can override the BGM controller currently in use by the game.

#### Options

- **Name**: Self-explanatory
- **Options Priority**: determines a priority level. The BGM controller with the lowest value has the highest priority. SQEX priorities are set as follows:
	- 0 = Event (cutscenes)
	- 1 = Boss (usually the last boss of each Disney and non-Disney world, during which neither Attraction nor Link music play)
	- 2 = MiniGame
	- 3 = Menu
	- 4 = Link
	- 5 = Attraction
	- 6 = Mission (scripted battles and scripted sequences)
	- 7 = Battle
	- 8 = Field
- **Options Store Behavior**: determines what happens after using the "Suspend BGM" and then the "Resume BGM" nodes on that BGM controller
- **Options Stop Behavior**: determines what happens after using the "Stop BGM" and then the "Play" nodes on that BGM controller
- **Options Play Fade in Time**: determines the fade during (in sec.) when using the "Play" node
- **Options Resume Fade in Time**: determines the fade during (in sec.) when using the "Resume BGM" node
- **Options Suspend Fade Out Time**: determines the fade during (in sec.) when using the "Suspend BGM" node
- **Options Stop Fade Out Time**: determines the fade during (in sec.) when using the "Stop BGM" node
- **Options Stay Suspend Time**: unknown
- **Options Unreference Asset**: unknown
- **Options Restore After Finish**: unknown

### Creating a new BGM controller from scratch

To create a BGM controller from scratch that can override currently playing BGM music, chain these nods in a blueprint:
1. **CreateBGMSlot** with "Options Priority" set lower than the currently BGM Slot's + "Options Restore After Finish" ticked
2. **Set Volume**
3. **Ready**
4. **Set** (requires a valid reference to a `SQEXSEADMusic` object)
5. **Play**