```
PIN 5 to Gnd
PIN 6 to Vdd
PIN 7 to CHIPINO PIN SS (A5)
PIN 8 to NC
PIN 9 to Gnd
PIN 10 to Switch/Resistor Connection
PIN 11 to NC
PIN 12 to NC
PIN 13 to NC
PIN 14 to NC
PIN 15 to NC
PIN 16 to LED1 Anode
PIN 17 to LED2 Anode
PIN 18 to 5v

Switch connected to ground and 10k resistor, 10k resistor to 5v.
LED1 and LED 2 each Cathode to ground through 1k ohm resistor.

*/
```

The header file for SimpleC is included next using quotation marks since the file is included in the same directory as our main C file.

```
#include "simplec1.1.h"
```

The main loop of code is next and starts off with two initialization functions from the SimpleC library. The init_micro function establishes the I/O setup and then the spi_init function creates the necessary settings for using the hardware SPI port.

```
void
main(void)
{
init_micro();
spi_init();
}
```

The first function dedicated to the MCP23S08 is used to set the pins to their proper input/output state by controlling the IODIR directory. This label IODIR is defined in the simplec1.1.h file. The settings are similar to a PIC in that a 1 is an input and a 0 is an output. So the 8 pins on the MCP23S08 are set to make the GP0 pin an input and the rest are outputs.

```
WR_MCP23S08 (IODIR, 0x01);    // Setup pins
```

The continuous loop of code is contained in a while loop. The first step is to create the local 8-bit variable y and preset it to 1.