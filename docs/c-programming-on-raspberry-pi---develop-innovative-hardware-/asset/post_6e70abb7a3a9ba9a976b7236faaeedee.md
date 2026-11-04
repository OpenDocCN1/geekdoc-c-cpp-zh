
```
/*-------------------------------------------------------------
                         DISPLAY TEXT ON LCD
                         ==================

In this program an LCD is connected in 4-bit mode to Raspberry Pi.
The text Raspberry Pi is displayed at row 0. Also, text Computer
is displayed at row 1

Author: Dogan Ibrahim
File  : LCDText.c
Date  : December 2020
-------------------------------------------------------------*/
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

//
// Start of MAIN program
//
int main(void)
{
        int lcd;

        wiringPiSetupGpio();
        lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
        lcdClear(lcd);

        lcdPosition(lcd, 2, 0);
        lcdPuts(lcd, "Raspberry Pi");
        lcdPosition(lcd, 4, 1);
        lcdPuts(lcd, "Computer");

}
```

Figure 6.3 Program LCDText.c

The program is compiled and run as follows (Notice the two libraries used):

```bash
gcc -o LCDText LCDText.c -lwiringPi -lwiringPiDev
sudo ./LCDText
```

The text is displayed on the LCD as follows:

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_184_0.png)

## 6.4 ➜ Project 2 – Second counter

### Description:

This is a second counter project, which counts up every second and displays on the LCD.  
The data is displayed as follows:

|  |  |
|---|---|
| **SECONDS:** | &lt;displayed on the first row&gt; |
| **nn** | &lt;displayed on the second row&gt; |

### Aim:

This project aims to show how text and numeric data can be displayed on the LCD.

### Circuit diagram:

The circuit diagram of the project is the same as in Figure 6.2.

### Program listing:

### wiringPi

Figure 6.4 shows the program listing (Program: **LCDSeconds.c**). At the beginning of the program, the connections between Raspberry Pi and LCD are defined as in the previous project. The variable **count** is initialised to 0 and is then incremented every second and displayed on the LCD using function **lcdPrintf**.

```c
/*-----------------------------------------------------------
                         LCD SECONDS COUNTER
                         ==================

In this program an LCD is connected in 4-bit mode to Raspberry Pi.
The program counts up every second and displays on the LCD

Author: Dogan Ibrahim
File   : LCDSeconds.c
Date   : December 2020
------------------------------------------------------------*/
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

//
// Start of MAIN program
//
int main(void)
{
    int lcd, count = 0;

    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    lcdClear(lcd);
    lcdPosition(lcd, 0, 0);
    lcdPuts(lcd, "SECONDS:");
    while(1)
    {
        lcdPosition(lcd, 0, 1);
        count++;
        delay(1000);
        lcdPrintf(lcd, "%d", count);
    }
}
```

Figure 6.4 Program LCDSeconds.c

## 6.5 • Project 3 – Creating a custom character

### Description:

In this project, we will create an up arrow as a custom character and display it on the LCD.

### Aim:

The project aims to show how a custom character can be created and displayed on the LCD.

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

Figure 6.6 shows the program listing (Program: **LCDcustom1.c**). Function **DisplayCustom** is called from the main program and displays the up arrow. Notice the index ranges from 0 to 7. It is the memory index where the custom character is saved.

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

### Circuit diagram:

The circuit diagram of the project is the same as in Figure 6.2.

### Program listing:

### wiringPi

The GPIO numbering scheme is used in this program (as opposed to the wiringPi numbering scheme). The custom characters are created using the **GLCD Font Editor** as in the previous project. Figure 6.7 shows the custom characters together with their pixel definitions.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_189_0.png)

The program listing (Program: **LCDcustom2.c**) is shown in Figure 6.8. The four custom characters are defined at the beginning of the program. Function **DisplayCustom** saves the character arrays **uparrow**, **downarrow**, **leftarrow**, and **rightarrow** in indexes 0, 1, 2, and 3 respectively. The arrows are then displayed with a one-second delay between each output. The result is four arrows displayed next to each other (up, down, left, and right).

```c
/*--------------------------------------------------------------
                 DISPLAY MULTIPLE CUSTOM CHARACTERS
                 ==================================

In this program an LCD is connected in 4-bit mode to Raspberry Pi.
The program displays up, down, left and right arrows

Author: Dogan Ibrahim
File  : LCDcustom2.c
Date  : December 2020
--------------------------------------------------------------*/
#include <wiringPi.h>
#include <lcd.h>

};

char rightarrow[8] = {
    0b00000,
    0b00100,
    0b00010,
    0b11111,
    0b00010,
    0b00100,
    0b00000,
    0b00000
};

//
// Display the custom character
//
void DisplayCustom(void)
{
    lcdCharDef(lcd, 0, uparrow);
    lcdCharDef(lcd, 1, downarrow);
    lcdCharDef(lcd, 2, leftarrow);
    lcdCharDef(lcd, 3, rightarrow);

    lcdClear(lcd);
    lcdPutchar(lcd, 0);
    delay(1000);
    lcdPutchar(lcd, 1);
    delay(1000);
    lcdPutchar(lcd, 2);
    delay(1000);
    lcdPutchar(lcd, 3);
    delay(5000);
}
//
// Start of MAIN program
//
int main(void)
{
    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    DisplayCustom();
}
```

Figure 6.8 Program LCDcustom2.c

## 6.7 • Project 5 – Displaying current date and time

### Description:

In this project, current date and time are displayed on the LCD. Data is displayed on the top row, while time is displayed on the bottom row.

### Aim:

This project shows how current date and time can be extracted and displayed on the LCD.

### Circuit diagram

The circuit diagram of the project is the same as in Figure 6.2.

### Program listing:

### wiringPi

Figure 6.9 shows the program listing (Program: **LCDDateTime.c**). The program reads the current date and time, formats them using function **strftime** and stores them in character arrays **CurrentDate** and **CurrentTime** respectively. The cursor is set to the top row and the current date is displayed. Similarly, the cursor is set to the bottom row and the current time is displayed. The format of the display is as shown in the following example:

```
22-12-2020
10:20:45
```

```c
/*-------------------------------------------------------------
                         DISPLAY TEXT ON LCD
                         ===================

In this program an LCD is connected in 4-bit mode to Raspberry Pi.
The program displays the date and time in the following format,
where the display is updated every second:

            dd-mm-yyyy
            hh:mm:ss

Author: Dogan Ibrahim
File   : LCDDateTime.c
Date   : December 2020
-------------------------------------------------------------*/
#include <wiringPi.h>
#include <lcd.h>
#include <time.h>
```
