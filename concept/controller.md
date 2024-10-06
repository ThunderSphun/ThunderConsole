# ThunderConsole Controller

The controller consists of 8 controls. There are 6 regular buttons, namely A, B, C, D, Meta and Bumper. The other controls are Trigger and Joycon.  
These last two have variable outputs. The Trigger has outputs ranging from 00 to FF, where 00 is not pressed and FF is fully pressed.  
The Joycon is a bit more complex, as it uses a reference angle, but the range of the Joycon output is from 0000 to FFFF.  

## Joycon

As stated the Joycon has a range from 0000 to FFFF. In case this precision is not needed the lower byte can be discarded.  
This value can be gotten from memory address $FF82 - $FF83. The reference angle can be set at address $FF84 - $FF85. This reference angle can be used to set a custom up. If the Joycon is pushed straight up, with the reference angle set to straight down, the angle will be 8000. if the reference angle were to be straight left, the angle would have been 4000.  
This reference angle can be changed to change the angle read from the Joycon. The reference angle is always measured from straight down the controller case, meaning the reference is the only way to get the actual angle the Joycon is facing.  
The Joycon is considered angled when the stick is about halfway turned, this way any potential drift that may exist will not be an issue.

## Trigger

The Trigger has 256 possible values. where 0 is considered not pressed and 255 fully pressed. This value can be read from memory address FF81.  

## Buttons

There are 6 buttons on the controller, so lets first focus on the most important group of buttons, the control buttons.  
This group consists of the A, B, C, D buttons, and are placed in a plus shape. The order of the buttons is like this:  
|||
|-|-|
|A|Top|
|B|Bottom|
|C|Left|
|D|Right|

Next is the Meta button, a button which doesnt have a clear meaning, so developers can be free to assign functionality to it as they please, for example a menu button or a restart button.  

Finally there is a Bumper button. This is again a button with less meaning, but it is easier to press whilst activly using the controller than the meta button.

## Controller Byte

There is a controller byte located at memory address FF80. This byte holds the current state of the controls on the controller.  
|bit|control|
|-|-|
|0|Button A|
|1|Button B|
|2|Button C|
|3|Button D|
|4|Joycon considered angled|
|5|Bumper|
|6|Trigger not 0|
|7|Meta|
