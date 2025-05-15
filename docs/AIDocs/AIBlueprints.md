---
title: TresGame Whitepages - AI
---



[Back to index](docs/index.md)

[Back to AI Overview](docs/AIOverview.md)

# **Blueprints:**

<ins>Get/Set Blackboard Keys in BP</ins>: You can get/set an AI’s blackboard key in a blueprint.
* Key Name, even though is a ``name`` variable in the blueprint, means the actual name of the blackboard key you are trying to find. If you want to find a certain key, you’d have to look at the blackboard, and find out what type of variable the key is.  
* Don’t use a ``blackboard key`` variable type in a regular blueprint.  
* Example: Finding the target actor key of an enemy.





<br/><br/>
<ins>Running an EQS inside a BP</ins>: If you want to run an eqs inside a BP for whatever reason, you may do so. You could use this to check for certain conditions in a manager, for example.
  



<br/><br/>
<ins>BTService\_BlueprintBase</ins>: This is how you make custom bt nodes using blueprints to run in your behavior tree, which allows you to execute logic and pass variables through the blackboard.Make sure when making a blueprint for a bt service <ins>**you use the</ins> ``BTService_blueprintbase`` <ins>class, do not use the regular BT\_Service class**</ins> (this is only for C++). You can create a blueprint service to run in a Behavior Tree. 

* You can create a service to check on intervals, update blackboards, or update other things in the world, or report debug easily.  
* Use Event Receive Tick (for each tick) and event receive activation (when the bt first gets to it)  
* Event receive deactivation is when the bt leaves that branch  
* Get blackboard key values like the example shows: This is where you use a ``blackboard key`` variable. Mark it instance editable so that the variable appears in the node on the behavior tree. On the behavior tree, after build, you will be able to set which key gets passed into the variable.  
  * *Note: Owner actor doesn’t work in kh3 for whatever reason, so you have to pass in selfActor through the bt/bb*  
* You can also set other variables to be exposed and set through a behavior tree.




<br/><br/>
<ins>BTTask\_BlueprintBase</ins>:  This is how you make custom bt nodes using blueprints to run in your behavior tree, which allows you to execute logic and pass variables through the blackboard. Make sure when making a blueprint for a bt task <ins>**you use the</ins> ``BTTask_blueprintbase`` <ins>class, do not use the regular BT\_Task class**</ins> (this is only for C++). You can create a blueprint task to run in a Behavior Tree. You’d usually use this to run background logic or set blackboard keys.

* Use event receive and finish execute to finish it properly, you must have finish execute. This allows you to set success/fail conditions for the BT to know if the task succeeded  
* In the example below, “ActorClass” is a public variable, allowing me to set the class from the BT to whatever I need




<br/><br/>
<ins>BtDecorator\_BlueprintBase</ins>: Make sure when making a blueprint for a bt decorator <ins>**you use the</ins> ``BTDecorator_blueprintbase`` <ins>class, do not use the regular BT\_Decorator class**</ins> (this is only for C++). You can create a blueprint decorator to run in a Behavior Tree.

* I honestly find it extremely rare to have to make a custom decorator. Square really went wild with making a ton of C++ decorators. Thus, I have not experimented in depth with every function or how exactly aborts and flow functions work.  
* Example below of checking if a specific ability is equipped


# Specific Node Documentation

-[Blackboard](Blackboards.md)  
-[Behavior Tree](BehaviorTree.md)  
-[States](States.md)  
-[Blueprint Nodes](AIBlueprints.md)  
-[Environmental Query System](EQS.md)
