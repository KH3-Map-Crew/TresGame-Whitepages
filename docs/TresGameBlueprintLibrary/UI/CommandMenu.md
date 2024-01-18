# Command Menu

[Back to index](index.md)

## Tres UI Add Action Command Mode

![Tres UI Add Action Command Mode Node](<images/2024-01-17 19_23_38-TresGame - Unreal Editor.png>)

Non-funcitonal reaction command prompts. Select from an enum `COMMAND_KIND` to specify text displayed in prompt.

Custom prompts can be added by means of data tables.

TODO: Need to specify the data table that contains this information.

### Pins
- Command Kind
  - An enum value of `COMMAND_KIND`. Determines the text displayed on the command.
- Command Kind Ex
  - Variation on Command kind? (Needs more details)

## Tres UI Delete Action Command Mode

![Tres UI Delete Action Command Mode Node](<images/2024-01-17 19_36_45-TresGame - Unreal Editor.png>)

Removes an existing reaction command prompt of the kind `COMMAND_KIND`.

### Pins
- Command Kind
  - An enum value of `COMMAND_KIND`. Determines the text displayed on the command.
- Command Kind Ex
  - Variation on Command kind? (Needs more details)
- Decision
  - ??? (Needs more details)