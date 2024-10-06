# ThunderConsole

## [Custom 8 bit processor](processor.md)

The processor has a 16 bit address bus, meaning the addressable space will be from 0000 to FFFF.  
The instructions are 8 bits, but many instructions have extra data as parameters.  
The ALU has a dual output, most of the time the second output will be the result of the opposite operation.  

## [Custom controller](controller.md)

The controller has a Joycon. This Joycon can be read from the code as an angle, between 0000 and FFFF. A reference angle can be set from code as well, usefull to define a custom up direction.  
When the Joycon is properly angled, the Joycon bit in the controller byte will be set.

There is a bumper button present, with a trigger button below it.  
The bumper button will set the bumper bit in the controller byte.
The trigger button has a range of 00 - FF, and when it is not 0, the trigger bit in the controller byte will be set.

There are also 4 buttons present to give input into the programs. These buttons are "A", "B", "C", "D", and are layed out in a plus shape.  
These will set bits A, B, C, D of the conroller byte respectively.

The final button on the controller is called the meta button.  
This button sets the meta flag of the controller byte.
