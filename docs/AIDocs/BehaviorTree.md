---
title: TresGame Whitepages - AI
---



[Back to index](docs/index.md)

[Back to AI Overview](docs/AIOverview.md)

# **Behavior Tree Guide**

Behavior Trees run the AI decision-making. They look like a tree and flow top to bottom, then left to right. 

Behavior Tree Basics:

* <ins>Root</ins>: **A Blackboard must be assigned. See blackboard section for more information.**  
* <ins>Composite Nodes</ins>: the grey nodes. You have to start with one. They control how a behavior tree flows. Should the behavior tree keep executing the same node, or should it execute left to right immediately?  
* <ins>Tasks</ins>: The purple nodes. These are generally states, but these are where each branch/leaf “ends”. Usually with a tresBTtaskAction node, which lets you set a state. Could also be a move to node, or a BTTask node you develop yourself (which is a task made out of a blueprint).  
* <ins>Decorators</ins>: Blue nodes. These nodes sit ontop of composites and tasks. These are gates for whether or not the tree should continue at that point. If they fail a decorator, then the tree starts flowing to another branch. They also include observers, which are very powerful. The decorators can abort other branches if the condition that was previously failed turns true. For example, a decorator can check the range from selfactor to targetactor.  
* <ins>Decorator Observers</ins>: a setting on every decorator that allows you to “abort” other tasks or branches (note that you cannot generally abort states unless you allow the state to be aborted by another type of state; more on that in state section).   
  * ``None``: No aborts, decorator simply acts as a gate  
  * ``Lower Priority``: If the conditions for this decorator become true, then abort whatever task/branch is running to the right of it, and snap it back to the left to this branch. (Highlighted nodes in blue can be aborted, sometimes highlights don’t show up)  
  * ``Self``: If the conditions for this decorator become false, then abort this branch and mark it as failed (and any children up to this decorator), meaning the tree will move on. (highlighted nodes in green can be aborted, sometimes highlights don’t show up)  
  * ``Both``: Observes for both lower priority and self.  
* <ins>Services</ins>: Green nodes. These also sit ontop of other nodes. They allow you to easily fill or change blackboard keys through ticks at set intervals. For example, you can run an eqs to determine the targetactor.

# Composite nodes:

* <ins>Selector</ins>: Finds the first child that succeeds. If that child succeeds, then the selector keeps running that child again. It will keep running that child until it fails. If that first child fails, it tries the next child. If that child succeeds, then it trieds the first child again, then the second. If both fail, then the selector is considered a fail, and it moves on. Generally, success means passing decorators, but you can set blueprint tasks to succeed or fail.  
* <ins>Sequence</ins>: Runs each child in a row. If a child fails, then the sequence fails and stops at that child and does not attempt to run the rest of the child. Example: child 1 fails, child 2 is not attempted.  
* <ins>Parallel</ins>: Run a purple task node (usually a state) alongside other logic. Using parallels is generally not considered good bt design. However, because we are limited by states in KH3, you might need to use these to spawn logic or management actors (but you could also spawn those or run logic in anim notifies).  
* <ins>Custom Composite (Tres “unknown composite”)</ins>: Gives you 3 options, ``first success``, ``first failure``, and ``last node completes``. First success is a selector (who know why they felt the need to remake these). It runs till it finds the first success, and then runs it again. First failure means it runs each node left to right until it fails, which then returns fail. “	  
  * ``Last node completes`` is what makes this composite important. “Last node completes” runs each node left to right, regardless of if any of the children fail. If child 1 and 2 fail, child 3 will still be attempted. This is called an **unconditional sequence**.  
* <ins>Random</ins>: Chooses a child at random. You can assign the probabilities using weights. I believe the weights are ratios, so you could use .33 .33 .33 or 1 1 1 for even distribution of children ((I’m 80% sure it filters out failing children automatically, but I could be wrong)). 

# Tasks:

* <ins>UE nodes</ins>: You generally won’t use the ue base nodes (except for run behavior).  
* <ins>TresTaskAction</ins>: Lets you set a state. You can also set a target actor.  
* <ins>TresTaskMoveTo</ins>: Moves the pawn to the location. You can use any actor, comp, or vector.  
  * Locomotion Defintion: allows you to use a different move state than the one set as the default in the pawn. Leave it as none to use the default set in the pawn.  
  * Use avoidance: Tries to avoid other actors while moving around  
  * Use path following: Uses navmesh to get to its destination. If you leave this unchecked, then it might get stuck on a wall it has to navigate around.  
  * Precise Arrival: Allows greater range for arrival rather directly on point.  
  * Abort time to keep moving: I’m not 100% sure what this does, but I think it allows the pawn to update its destination without using another move to task or quickly stopping, ie it keeps moving towards new destinations.  
  * Blackboard/Blackboard Key (the farthest down bb key): This is the most important, the destination. Can be a vector, an actor, or a component  
* <ins>Run Behavior</ins>: runs a behavior tree  
* <ins>RunEQS</ins>: Runs an environmental query (Note: Usually you’d rather use a ``service`` than a task node for this, please view Services for ``RunEQSQuery``)  
  * Note: don’t bother with the depreciation nodes, you can leave them default  
  * EQS Query: Which eqs will you run  
  * Result: Which bb key to fill? NOTE: You must choose a key that matches the EQS. ie if its an eqs that returns an actor, use an ``actor`` blackboard key. If it returns a vector, use a ``vector`` key.  
  * ActionEQS: You could use bb keys to dynamically set eqs to be run, but I have never seen them actually use this, nor I have used this.  
* <ins>BlackboardObjectModifier (and other BBxModifiers)</ins>: modifies the blackboard key to what you want or need, such as setting an int key to what you need, or adding or subtracting from it.  
* <ins>Wait</ins>: Makes the AI wait/idle for a set time (You can abort this easily as almost every state can abort idle)

# Decorators:

* <ins>Range check</ins>: Runs check on range between two actors, components, vectors, or combination between the two. Pass/fail based on conditions  
  * Starting point: bb key (such as selfactor)  
  * Target: bb key (such as targetactor)  
  * Use distance/source bounds: I generally leave this checked, though I am not sure what it does exactly.  
  * RangeMode: 2d, 3d, Z (up/down only)  
  * Range Value Setting: Min Max Range, Minimum is atleast x amount away or farther \= true. Maximum is x amount away or less \= true.  
  * You can use numbers or blackboard keys for the test  
  * Example: This checks that the target/lockoncomp of the target is at minimum 500 units away or more. If so, proceed and use thundaga. If the lock on comp comes closer to selfactor than 500 units, abort that task/stop trying to run it.  
* <ins>Validate Action</ins>: Validates that the state can be executed before attempting to run the state. You can check “execution” (which includes ability equipped and mp for npcs), location (range set in the state), orientation (angle/rotation params set in the state).  
  * Action: put the state here  
  * Use blackboard definition: only if you want to use a state “class” to check from a blackboard key instead of a set state. You most likely will not ever need this  
* <ins>Tres State check</ins>: Checks if the pawn’s state enum matches atleast one of the state enum you list. The blackboard key lets you test target actor, self actor, or any other pawn actor.  
* <ins>Cooldown/TagCooldown</ins>: Allows you to set cooldowns for those branches after they’re executed. Using tagcooldown alongside “settagcooldown” allows you to use tags so that multiple branches can be put on cooldown from one tag.  
* <ins>Loop</ins>: forces multiple executions of a node (useful in sequences) unless it’s aborted  
* <ins>Blackboard</ins>: Allows you to pick a blackboard key and check against it. Observers make these powerful, as you can set blackboards easily through blueprints, allowing you to extend and control your behavior trees through anim notifies, managers, level scripts, or anything else blueprint related.  
  * For bools, is true or false?   
  * For int, is int greater/less than or \= to number?  
  * Does string \= str'?  
  * Is actor bb key valid? (key is still filled or actor in key still exists?)

# Services:

* <ins>Run EQS Query</ins>: this is generally what you will be using mostly when it comes to services. Runs an environmental query, which scans for locations or targets.  
  * EQS Query: Which eqs will you run  
    * Configs: Note that <text style="color: red">**you must dummy your EQS correctly in order to have configs show up**. **If you do not, your eqs will not run, and your BT will probably not run.**</text> The eq configs allow you to pass in your own parameters into an environmental query. If you want to learn more, look at the EQS guide, but for BT, you must make sure it matches what an EQS example looks like from a Square Enix made node. <ins>**If you dummy the EQS correctly, they should automatically populate the environment configs**</ins>.  
    * Use UAssetGui to find what an EQS config should look like in a BT. You can also attempt to backwards import an EQS. See C-Paz’s guide on backwards importing eqs. (Some EQS break the editor).  
    * To dummy the EQS properly if you cannot backwards import, make any generator, add any test, and add the correct “AI data label” types, with the matching name. See example below on the EQS side. *Note: To make EQS, you have to enable EQS in the editor preferences*  
    * Some EQS can be backwards imported from cooked into the editor. C-Paz has a guide on this. Many of them unfortunately crash the editor, however.  
  * Blackboard Key Result: Which bb key to fill? NOTE: You must choose a key that matches the EQS. ie if its an eqs that returns an actor, use an actor key. If it returns a vector, use a vector key.  
  * ActionEQS: Unknown, but I do not think it is used. (My only guess is that you could use bb keys to dynamically set eqs to be run, but I have never seen them actually use this).  
  * Invalidate Key: If the EQS fails to return anything, should the key also be cleared?  
  * Service Interval: How often to run this service  
* <ins>Gameplay Focus</ins>: This makes the pawn running the BT “focus” on whichever actor bbkey you place. This purely means they pretty much look at them/turns their head towards the actor, even if running or walking sideways.


# Specific Node Documentation

-[Blackboard](Blackboards.md)  
-[Behavior Tree](BehaviorTree.md)  
-[States](States.md)  
-[Blueprint Nodes](AIBlueprints.md)  
-[Environmental Query System](EQS.md)
