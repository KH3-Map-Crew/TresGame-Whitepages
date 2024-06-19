---
title: TresGame Whitepages - AI
---

# Flowmotion

[Back to index](../index.md)

Flowmotion uses actors in a straightforward manner. Most only requiring to place down a specific actor.

## Wall running (Static mesh)

On any actor with a static mesh component, search for `Enable Wall Run` and enable that flag. This will allow the player to run up the mesh.

TODO: Other flags exist for similar properties, but require additional research and documentation.

## Pole (Tres Pole actor)

Actor that handles pole spins. The player rotation point is ~202 units above the "origin" of the actor.

Be mindful of nested compoment placement as some might not have zeroed relative coordinates

### Vertical
By default, all pole actors are vertically oriented.

Example in practice:
![vertical pole](Flowmotion/images/2024-06-19%2018_54_26.png)

### Horizontal
All that's required for a horizontal pole, is to open the pole component and flipping the `isHorizontal` flag.

Example in practice:
![horizontal pole](Flowmotion/images/2024-06-19%2018_58_31-TresGame%20-%20Unreal%20Editor.png)


## Stepping stone (Tres Hop actor)

Be mindful of nested component placement as some might not have zeroed relative coordinates

Nothing special here. Simply place on your mesh of choice.

Example in practice:

![hop actor](Flowmotion/images/2024-06-19%2019_00_24-TresGame%20-%20Unreal%20Editor.png)

## Rail (Tres Rail Slide actor)

The most complicated setup, but still not too difficult.

To connect slide actors, you will need to link connections through the `Connections` and `Links from` fields.

`Connections` linking to the *next* point in the rail slide, and `Links from` being the *previous*. This is because you can configure the rail slide to be either one way, or bi-directional.

You can also configure restrictions and other parameters while on the rail as well.

![fields](Flowmotion/images/2024-06-19%2019_18_45-TresGame%20-%20Unreal%20Editor.png)

Here is an example in practice:

![point A](Flowmotion/images/2024-06-19%2018_56_15-TresGame%20-%20Unreal%20Editor.png)
![point B](Flowmotion/images/2024-06-19%2018_56_43-TresGame%20-%20Unreal%20Editor.png)
![point C](Flowmotion/images/2024-06-19%2019_14_15-TresGame%20-%20Unreal%20Editor.png)