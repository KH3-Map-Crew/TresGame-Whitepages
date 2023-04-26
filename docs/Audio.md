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

### Suspend BGM

Suspends the currently playing BGM. If resumed, will continue from the time it was suspended.

### Resume BGM

## SQEXSEADBGMSlot Controller

Maintains a BGM slot. Can be accessed through a few methods.

### Get playing BGMSlot Controller

Retrieves the active BGMSlot controller.

### Get BGM Slot Controller

Given the name of a BGMSlot, retreive it's controller.

### Set

Given a controller, set the currently playing track for that BGMSlot.
