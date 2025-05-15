---
title: TresGame Whitepages - AI
---



[Back to index](../index.md)

[Back to AI Overview](AIOverview.md)

# States

States define the actions a character takes. The behavior tree tells the AI which action to take, while the state defines the mundane of what that action is, and how it is carried out. If you are coming from working on player characters, you are probably familiar that states and the state machine are largely “hidden” behind C++. While this is somewhat true for AI, we can create states and choose which states to run based off of behavior trees, which pretty much eliminates this problem completely.




<br/><br/>
<ins>Blueprint States</ins>: States can be custom made by creating blueprint classes off of C++ parent classes. This allows you to make any state and use it on any pawn, which makes your options limitless. For the most part, you can use the generic non-pawn listed states for any pawn. Unfortunately, you cannot directly apply pawn specific states to other pawns. For example, you cannot force a large body to run goofy tornado. The goofy tornado state is expecting the goofy pawn, and thus will not attempt to run on a large body, even if you call for it in the large body’s bt. <text style="color: red">It will either fail that BT node or softlock the ai.</text> However, you can recreate goofy tornado with a largebody using a mix of BP state and regular BPs.




<br/><br/>
<ins>Pre-Existing States/Dummies</ins>: If you are simply recreating/re-arranging AI from a vanilla source, you can simply create dummy states for the BT. Just follow the square name/folder path, and you can make the state out of any bp State. For locomotion states, make sure to use a locomotion state as the base class. You cannot backwards import these cooked because they are bp; you must dummy them manually or using a dummier tool.




<br/><br/>
<ins>Blueprint Functions/Events</ins>: None of the states have blueprint functions or events that you can override or use, so there is no point in directly applying blueprint logic inside the state bp itself. (States are objects, not actors) The state bp is useful because we can edit the default variables. If you need more complicated logic, you can use the BT tasks or services to spawn blueprint managers that move the pawn, spawn projectiles, etc. (or use anim notifies)




<br/><br/>
<ins>**TresAttackDefinitionMelee**</ins>: This is pretty much the best state and will make up the bulk of what you need or use. If you are using an npc, you can use the npc version. This state lets you set the animation to play, and lasts as long as the animation lasts unless the pawn is put in damage or aborted through some other method. Press on class defaults to bring up the variables in order.

* Note on the usability of this state: I generally <ins>**use this state for almost everything.**</ins> While the state is titled “melee”, it really just is a play anim state, which makes it simple for extending and customizing. Even for more complicated endeavors, such as a boss move that spawns multiple projectiles far away from the player, I would still use this in combination with BP managers in a BT to spawn the projectiles while running this state.  
* Attack Anim Data: anim sequence  
* Min/Max distance: what is the min max distance it can use this state from its target? Note: if you are going to use these bools, make sure to use a validate attack decorator in the Bt  
* Npc AI Info\>attackdeftype/ability kind: for npcs, checks if they have the ability equipped, if they have enough mp, and then subtracts mp when they run this state. Note: if you are going to add an ability check, you must use a validate attack decorator in the BT  
* Viable states: Array of state enums that allow you to transition into this state. Example: For a normal enemy melee attack, you would probably put AI move, Idle, and Turn, as these are acceptable states to abort in order to use this state. <ins>**If you leave this blank, the state might not get activated.**</ins>  
* MyStateID: This single enum defines what “type” of state this state you are creating is. For example, if it is an attack, you would put AI Attack (generally do not want to use Attack or Fire or other state id). 




<br/><br/>
<ins>Other states</ins>:

* TresLocomotion(Land/Flying/other): These are for movement, and you could also add attack id’s to them in the animation if you want them to be attacks.  
* TresAttackDefinitionRanged: Allows you to spawn a single projectile from the pawn’s projectile set. Easy to use if you only need one spawned from a set point on the pawn.  
* TresNPCAttackDefinitionMagic: Follows the magic set and allows you to spawn magic without fiddling with animations, if the pawn is setup to use this.


# Specific Node Documentation

-[Blackboard](Blackboards.md)  
-[Behavior Tree](BehaviorTree.md)  
-[States](States.md)  
-[Blueprint Nodes](AIBlueprints.md)  
-[Environmental Query System](EQS.md)
