---
title: TresGame Whitepages - AI
---



[Back to index](../index.md)

[Back to AI Overview](AIOverview.md)

# **EQS GLOSSARY**  
Create an environmental query by right clicking, hovering over AI, and selecting EQS. If eqs doesn’t appear, you need to enable it in the editor preferences (4.17 considered it an “experimental” feature). It should then appear. When you create one, right click anywhere on the graph to create a generator node (grey node). Right click on that generator node to create a test node (blue node).



<br/><br/>
Contexts (*separate from the Context generator*): The type of ``items`` to test. It can be enemies, players, allies, or “items” (such as vertices). You can create Blueprint Contexts, see near the end for information. Example: Note the circle ``context``: it is centered around the context querier. You could also set it around another context. You can also use contexts that include multiple objects (such as tres\_enemies).


<br/><br/>
Generators: Generators give a set of items to test against. After running each test on every item, generators find the best item with the highest score and return the result. Example: Context Generator set to “enemies” with a basic distance test will return the farthest enemy.


<br/><br/>
Tests: These are the tests used to weigh potential candidates against each other. Tests can be set to filter or score.

## Generators

* <ins>Projection Data</ins> (setting on all generators): If you use any generators that generate any points via locations, <text style="color: red">**you must set this to navigation.**</text> If you do not, it will project points that the AI cannot reach, and you definitely do not want that. *Note: You don't need it for context or actors of class*  
* <ins>Actors of Class</ins>: Finds all of the actors of given class currently in existence. Base UE node. Context is more powerful, I would only use Actors of class for testing in engine. (This same picture from above is Actors of class: enemy pawn context). Notice how every enemy pawn is assigned weight.  
* <ins>Points (Circle, Box, etc)</ins>: Base UE node. Generates points around the given context.  
    
* <ins>Context</ins>: Finds all of the matching items at that point that belong to the group. Basically, it’s a “get all actors of class” type of generator, though you can use specific contexts such as enemies, specifically target, locations, specific locations, querier (self).  
    
* <ins>OnRing/OnRing 3D</ins>: Generates rings around the context. It’s like the basic circle in base UE generator, but allows for multiple circles at once. This is generally what tres uses.  
* <ins>Using multiple generators</ins>: You would only use multiple generators if you have a filter test. Second generator kicks in if all of the items on the first generator fail. It follows left to right. It does not evaluate their scores against each other.  
* <ins>Composite</ins>: Lets you use multiple generators in one node.This additionally lets you rank each item from every generator against each other, which solves the problem written above. I’ve never used it in game, but it’s possible if you go wild with this it might tank performance. 


## Tests


* <ins>Filter</ins>: Test setting \- filters out items based on given parameters. Example: setting distance to filter min of 300 means items will only be considered if at least 300 units away or more from the context.  
    
    
* <ins>Score</ins>: Test setting \- Scores judge the items. Each test scores each item relative to the context. The items that match the closest to the test get the highest scores. You can change the scoring to inverse, or other equations (including some equations square made that were left out of the engine), and use clamps. You can also set tests to both score and filter.  
    
* <ins>Distance</ins>: Base UE distance. Search UE docs for more info. Example: Find point farthest away from the enemy out of points generated around mickey. ((Side note: use Z (absolute) for vertical distances, regular Z gives me weird returns.))  
    
* <ins>DOT</ins>: Base UE Dot product (useful for checking angles). Search UE docs for more info  
* <ins>Targeting Test</ins>: Checks to see if context is targeting that target. It’s a range filter rather than bool because you can check how many of said context are targeting that target. For example, context generator of enemies \+ targeting test context of allies lets you test how many allies are targeting each enemy. *Great way to get the player’s yellow target icon through bp if you need\!* 
  * Example: Check if the player is targeting each enemy (and how many players, though obviously that part is redundant. I assume it was designed for mobs to check how many are targeting each party member.) If the amount of players targeting that enemy \= 0, then it’s an acceptable match.  
* <ins>IsTargetingContext</ins>: Does the item (should be a charpawn) have its target set to the context? Example: Test filters out any targets that ARE targeting the querier, if you wanted not targeting, you would check bool match (which would mean filter the items down to only enemies targeting the querier)  
* <ins>MinDistance</ins>: (tres node) ? I’m still confused on how this one works. Best avoid it since you can use distance for what I believe it is supposed to do.
  * I'm pretty sure it gets the closest distance to the querier when set to linear, but you can do the exact same thing using distance: inverse linear.
* <ins>Return Target</ins>: checks if the enemy (or other context) is targeting the querier (they didn’t rly need this when they have targeting context)  

## Blueprints

[EQS in Blueprints](AIBlueprints.md#eqs-blueprints)

Press the link above for creating BP contexts, running eqs in a bp, creating an eqs pawn.

# Specific Node Documentation

-[Blackboard](Blackboards.md)  
-[Behavior Tree](BehaviorTree.md)  
-[States](States.md)  
-[Blueprint Nodes](AIBlueprints.md)  
-[Environmental Query System](EQS.md)
