```
```c
char arrow[8] = {
0b00100,
0b01110,
0b10101,
0b00100,
0b00100,
0b00100,
0b00100,
0b00100
};
```
```

Figure 6.6 shows the program listing (Program: **LCDcustom1.c**). Function **DisplayCustom** is called from the main program and displays the up arrow. Notice the index ranges from 0 to 7. It is the memory index where the custom character is saved.

```
```c
/*---------------------------------------------------------------
                         DISPLAY CUSTOM CHARACTER
                         ========================

In this program an LCD is connected in 4-bit mode to Raspberry Pi.
The program displays an up arrow as a custom character

Author: Dogan Ibrahim
File : LCDcustom1.c
Date : December 2020
---------------------------------------------------------------*/
#include <wiringPi.h>
#include <lcd.h>


//
// Connections between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10


int lcd;


//
// Define the custom character (up arrow)
//
char arrow[8] = {
                         0b00100,
```
```