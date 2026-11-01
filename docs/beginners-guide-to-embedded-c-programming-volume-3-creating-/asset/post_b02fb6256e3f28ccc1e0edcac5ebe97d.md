
![](img/910b145bee7ca8076318eafbe6d13997_138_0.png)

Figure 8-2B: CHIPINO Module Breadboard Setup

## Software

The software initially writes 10 bytes of data to the EEPROM and then it reads back those 10 bytes to display them on the LCD. If the first part doesn’t work then the second part will display whatever was left in those EEPROM locations.

```
/* SPI_EEPROM example using the Microchip 25LC020
The program writes to the first 10 locations
and then reads back those writes and displays
them on the LCD.
```

- SPI EEPROM
- PIN 1 - RA5 (CHIPINO AN4 pin)
- PIN 2 - RC4 (CHIPINO PIN 3)
- PIN 3 - V+
- PIN 4 - Gnd
- PIN 5 - RC5 (CHIPINO PIN 2)
- PIN 6 - RC3 (CHIPINO PIN 4)
- PIN 7 - V+
- PIN 8 - V+

- LCD
- PIN 1 - Gnd
- PIN 2 - V+
- PIN 3 - Gnd
- PIN 4 - RB4/CHIPINO Pin 12 (RS)
- PIN 5 - Gnd
- PIN 6 - RB5/CHIPINO Pin 13 (EN)
- PIN 7 - NC
- PIN 8 - NC
- PIN 9 - NC
- PIN 10 - NC
- PIN 11 - RB0/CHIPINO Pin 8 (DB4)
- PIN 12 - RB1/CHIPINO Pin 9 (DB5)
- PIN 13 - RB2/CHIPINO Pin10 (DB6)

```
PIN 14 - RB3/CHIPINO Pin11 (DB7)
*/

#include "simplec_1.1.h"
#define number 0x30

void
main(void)
{
init_micro();    // Initialize PIC16F886
spi_init();      // Initialize SPI Peripheral
lcd_init();      // Initialize LCD Display

//*** Load Data in EEPROM ***
while (1==1)
{
    for( char addr = 0; addr < 10; addr = addr + 1) // Loop 10 times
    {
        char data = addr;      // addr value is data for SEEPROM
        WR_BYTE (addr,data);   // Write to SEEPROM
        pause (10);            // Delay 10ms after each write
    } // End For

//*** Continuous Loop to Read and Display Data ***
    for( char addr = 0; addr <10; addr = addr + 1) // Loop 10 times
    {
        lcd_clear();           // Clear LCD screen
        lcd_goto(0);           // select first line
        lcd_text("Address / Value"); // Display header
        char b0 = RD_BYTE (addr); // Read from SEEPROM
        lcd_goto(0x40);        // Select second line
        lcd_symbol(addr + number); // Display value read from
                           //EEPROM on LCD
        lcd_text(" / ");
        lcd_symbol(b0 + number); // Display value read from
                           //EEPROM on LCD
        pause (250);           // Delay 250 msec to see count
    } //End For
} //End While
} //End Main
```

## How it Works

The header block describes the project and then also describes the connections.

```
/* SPI_EEPROM example using the Microchip 25LC020
The program writes to the first 10 locations
and then reads back those writes and displays
```

The first action the code does is load the data into the EEPROM. This is done in a for loop that cycles through 10 times.

```
//*** Load Data in EEPROM ***
while (1==1)
{
    for( char addr = 0; addr < 10; addr = addr + 1) // Loop 10 times
    {
```

Within the for loop, the data to be sent to the EEPROM will be the same as the address and also the same as the for loop counter value.

```
char data = addr;    // addr value is data for SEEPROM
```

Here is where the SimpleC library comes in. The WR_BYTE function takes the parameters and sends it to the EEPROM. The first parameter is the address and the second is the data byte. This function handles all the communication to the EEPROM. It takes time for the external EEPROM to complete the write so a delay of 10 milliseconds is added. That completes the initial write to EEPROM.

```
WR_BYTE (addr,data);    // Write to SEEPROM
pause (10);             // Delay 10ms after each write
} // End For
```

Now we loop through the memory to read each byte we just wrote to the EEPROM. We do this in a for loop again with the same 10 count. Most of this loop contains functions to control the LCD.

```
//*** Continuous Loop to Read and Display Data ***
for( char addr = 0; addr <10; addr = addr + 1) // Loop 10 times
{
```

The LCD is cleared and positioned at the beginning of line 1. Then the screen displays a header for the data “Address / Value” on the first line. These are all done with the SimpleC functions.

```
lcd_clear();            // Clear LCD screen
lcd_goto(0);            // select first line
lcd_text("Address / Value");  // Display header
```

Now the SimpleC function for reading the data is performed. A char variable b0 is created on the same line that executes the RD_BYTE function. This
function retrieves the data from the EEPROM at the address in the address parameter. The byte received is stored in the b0 variable.

```
char b0 = RD_BYTE( addr);   // Read from SEEPROM
```

Now that we have the data and already know the address, we position the LCD to the second line and then display the address value and the data value using separate lcd_symbol functions. The values are added to the constant “number” so the value sent to the LCD is the ASCII value for the value. This method works because all the values are single digit values.

```
lcd_goto(0x40);          // Select second line
lcd_symbol(addr + number);   // Display value read from
                           //EEPROM on LCD
lcd_text(" / ");
lcd_symbol(b0 + number);   // Display value read from
                           //EEPROM on LCD
```

A delay is added so we can easily read the values displayed on the LCD.

```
pause (250);          // Delay 250 msec to see count
} //End For
} //End While
} //End Main
```

## Next Steps

You can play with the first loop to change the data being stored and verify it works by monitoring the display. You can also expand the project to store more data but you’ll have to modify the way the data is displayed on the LCD because larger amounts of data mean address values larger than single digit.

## Project 2 – Inputs from MCP23S08

The MCP23S08 is a SPI I/O expander and is great for adding up to eight digital pins to your project by sacrificing the four SPI pins. This project doesn't use all eight but does use a few to show how to sense a switch with the MCP23S08 and then control LEDs based on the state of the switch. The communication between the PIC16F886 and the MCP23S08 is through the SPI peripheral. The SimpleC library has functions specific for this MCP23S08 chip so the code is easier to write.

## Hardware

The schematic is shown in Figure 8-3 and shows all the connections to the PIC along with the two LEDs and switch connected to the MCP23S08. The breadboard version is shown in Figure 8-4A using the CHIPINO Mini and Figure 8-4B uses the CHIPINO module. In this case I only show the CHIPINO Mini version of the breadboard setup. Power to the rails is supplied through the CHIPINO Mini module, which gets its power from the PICkit 2 programmer (not shown in picture). The upper power rail has ground on the outer space while 5v is on the inner rail. The lower power rail is the opposite. The two positive rails are connected together at the right side of the breadboard. The 10k resistor that connects to the switch appears to share the same hole as the wire, which it does in this picture. In reality the resistor was one hole higher but the drawing software wouldn't allow it so I left them sharing a hole.

![](img/910b145bee7ca8076318eafbe6d13997_144_0.png)

Figure 8-3: SPI Project 2 Schematic

![](img/910b145bee7ca8076318eafbe6d13997_144_1.png)

Figure 8-4A: SPI Project 2 Breadboard

```
PIN 12 to NC
PIN 13 to NC
PIN 14 to NC
PIN 15 to NC
PIN 16 to LED1 Anode
PIN 17 to LED2 Anode
PIN 18 to 5v

Switch connected ground and 10k resistor, 10k resistor to 5v.
LED1 and LED2 each Cathode to ground through 1k ohm resistor.
*/

#include "simplec_1.1.h"

void
main(void)
{
init_micro();
spi_init();
WR_MCP23S08 (IODIR, 0x01);   // Setup pins
while (1==1)
{
char y = 1;
y = RD_MCP23S08 (GPIO); // Read switch
y = y & 0x01;           // Mask all but bit 7
if (y==0)
{WR_MCP23S08 (OLAT, 0x40);}  // If switch idle light LED
else
{WR_MCP23S08 (OLAT, 0x80);}  // If switch pressed LED off
pause(10);
} //End While
} //End Main
```

## How it Works

The first part of the software is located between two comment indicators so this creates an information header. The operation is described along with a description of the electrical connections.

```
/***********
PIC16F886 SPI - MCP23S08 I/O expander
The program reads a switch connected to the MCP23S08 GP0 pin.
It lights the LED connected to GP7 if the switch is idle and
lights the LED connected to GP6 if the switch is pressed.

Connections
MCP23S08
PIN 1 to CHIPINO PIN 4 (SCK/RC3)
PIN 2 to CHIPINO PIN 2 (SDO/RC5)
PIN 3 to CHIPINO PIN 3 (SDI/RC4)
PIN 4 to Gnd
```
