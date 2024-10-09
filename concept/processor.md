# The ThunderConsole Processor

## Address space

The processor has a 16 bit address bus, meaning it can access memory from 0000 to FFFF.  
This memory is split into three regions, namely 0000 - 7FFF, 8000 - FEFF and FF00 - FFFF. The first region is located on the board, and will be RAM. The second region must be externally provided, and is meant to be ROM, but nothing prevents developers to write to that address space. The third region is a special region which is partially provided from the board and partially provided externally.  
The address bus is split up into pages of 256 bytes. This makes the higher 8 bits the page byte, and the lower 8 bits the offset byte.  
Some of these pages have special meaning.  
|min|max|name|description|
|-|-|-|-|
|`$0000`|`$00FF`|0-page|Some operations have variants which can only access this page, these operations are always faster.|
|`$1000`|`$13FF`|Bank 0|Can be bank switched for more storage space.|
|`$1400`|`$17FF`|Bank 1|Can be bank switched for more storage space.|
|`$7F00`|`$7FFF`|Stack |The stack can be used for temporary storage of variables. it grows downwards.|
|`$8000`|`$83FF`|Bank 2|Can be bank switched for more storage space.|
|`$8400`|`$87FF`|Bank 3|Can be bank switched for more storage space.|
|`$FF00`|`$FFFF`|MMRP  |The Memory Mapped Registry Page is a special page, where data about the system can be read from and written to.|

### MMRP

As stated earlier, MMRP is a special page, it is provided both by the board and externally. Reads and writes are first attempted on the board, when it is not present there, it will be searched externally.  
|byte|name|external|description|
|-|-|-|-|
|`$FF80`|Controller byte						|❌|Has the controller button flags stored. See [controller.md](controller.md#controller-byte) for byte layout.|
|`$FF81`|Controller Trigger value				|❌|The current value of the controller trigger button.|
|`$FF82` - `$FF83`|Controller Joycon angle		|❌|The current angle of the controller Joycon, in reference from the Joycon reference angle.|
|`$FF84` - `$FF85`|Controller reference angle	|❌|The relative up direction of the Joycon. Altho it is located on the board, it is intended that this is written to.|
|`$FFF0`|RAM Bank index							|✔️|This byte stores the index of bank 0 and 1. Bank 0 is stored in the lower nibble, bank 1 in the higher. When this is written to, a inaccessible interrupt is invoked to swap to the correct banks|
|`$FFF1`|ROM Bank index							|✔️|This byte stores the index of bank 2 and 3. Bank 2 is stored in the lower nibble, bank 3 in the higher. When this is written to, a inaccessible interrupt is invoked to swap to the correct banks|
|`$FFFC` - `$FFFD`|Generic Interrupt address	|✔️|The address to jump to when the interrupt instruction is executed.|
|`$FFFE` - `$FFFF`|Reset address				|✔️|The address to jump to when the processor is reset.|
