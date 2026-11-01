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