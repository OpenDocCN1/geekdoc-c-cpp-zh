```
```c
File  : Dice.c
Date  : December 2020
--------------------------------------------------------------*/
#include <wiringPi.h>
#include <stdlib.h>

#define OFF LOW
#define ON HIGH
#define Button 15                         // GPIO 14

#define D1 13
#define D5 0
#define D2 12
#define D6 9
#define D4 2
#define D3 3
#define D7 8

int LEDs[] = {13, 12, 3, 2, 0, 9, 8};         // GPIO 9,10,22,27,17,3,2

//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
        char k;
        for(k = 0; k < 7; k++)
        {
                pinMode(LEDs[k], OUTPUT);
                digitalWrite(LEDs[k], OFF);
        }
        pinMode(Button, INPUT);
}

//
// Display data on ports
//
void All_Off()
{
        char i;
        for(i = 0; i < 7; i++)digitalWrite(LEDs[i], LOW);
}

//
// Start of MAIN program
```
```