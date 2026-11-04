
| GPIO pin | wiringPi pin | Physical pin |
|---|---|---|
| 11 (MSB) | 14 | 23 |
| 9 | 13 | 21 |
| 10 | 12 | 19 |
| 22 | 3 | 15 |
| 27 | 2 | 13 |
| 17 | 0 | 11 |
| 3 | 9 | 5 |
| 2 (LSB) | 8 | 3 |
| 14 | 15 | 8 (Button) |

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_129_0.png)

Figure 5.14 Block diagram of the project

## Circuit diagram:

The circuit diagram of the project is as in Figure 5.15. 8 LEDs are connected to GPIO ports through 470 Ohm current limiting resistors. Notice the button can be connected in two different ways to a GPIO port. In Figure 5.16, the output of the button is at logic 1 and goes to logic 0 when the button is pressed. In Figure 5.17, the output of the button is at logic 0 and goes to logic 1 when the button is pressed. In this example, the second method is used. Thus, the GPIO pin is normally at logic 0 and goes to logic 1 when the button is pressed.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_0.png)

Figure 5.15 Circuit diagram of the project

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_1.png)

Figure 5.16 Button normally at logic 1

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_130_2.png)

Figure 5.17 Button normally at logic 0

## Program listing:

### wiringPi

The program listing of the project is shown in Figure 5.18 (Program: **UpDown.c**).

```
/*---------------------------------------------
BINARY UP/DOWN COUNTER
======================
In this program 8 LEDs are connected to GPIO ports through current
limiting resistors. Additionally, a button is used. The program counts
up/down in binary every 500ms. By default it counts up. When the
button is pressed it counts down as long as the button is kept pressed

Author: Dogan Ibrahim
File : UpDown.c
Date : December 2020
-------------------------------------------------------------*/

#include <wiringPi.h>
#include <stdlib.h>

#define OFF LOW
#define ON HIGH
#define Button 15        // GPIO 14
#define UP 0
#define DOWN 1

int LEDs[] = {14, 13, 12, 3, 2, 0, 9, 8};     // GPIO 11,9,10,22,27,17,3,2

//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
    char k;
    for(k = 0; k < 8; k++)
    {
        pinMode(LEDs[k], OUTPUT);
        digitalWrite(LEDs[k], OFF);
    }
    pinMode(Button, INPUT);
}

//
// Display data on ports
//
void Display(unsigned int No, unsigned int L)
{
    unsigned int j, i, m, p, r;
    m = L - 1;
    for(i = 0; i < L; i++)
    {
        j = 1;
        for(p = 0; p <= m; p++) j *= 2*j;           // Power of 2
        r = No & j;
        if(r > 0) r = 1;
        digitalWrite(LEDs[i], r);
        m--;
    }
}

//
// Start of MAIN program. When the button is not pressed, increment
// count. When the button is pressed, count down from the last value
//
int main(void)
{
        char j, count = 0;
        char Button_State;

        wiringPiSetup();
        Configure();

        while(1)
        {
                Display(count, 8);
                Button_State = digitalRead(Button);

                if(Button_State == UP)
                {
                        if(count == 255)
                                count = 0;
                        else
                                count++;
                }
                else if(Button_State == DOWN)
                {
                        if(count == 0)
                                count = 255;
                        else
                                count--;
                }
                delay(500);
        }
}
```

Figure 5.18 Program UpDown.c

At the beginning of the program, an array called LEDs is set up to store the port numbers of the LEDs used in the project. Name **Button** is assigned to GPIO port 14, and names **UP** and **DOWN** are assigned to 0 and 1 respectively. Global variable **count** is initialised to zero. The GPIO ports where the LEDs are connected are then configured as output ports, and the GPIO port where the **Button** is connected is configured as an input port. Inside the main program, function **Display** is called and **count** is sent as the argument. The state of the **Button** is then read: if the **Button** is not pressed (**Button_State** equal to **UP**) then an UP count is performed. If on the other hand the **Button** is pressed, (**Button_State** equal to **DOWN**) a DOWN count is performed. Notice variable **count** is reset at the end of the counts. i.e. during an up count when the count reaches 255 it is reset to 0 on the next cycle. Similarly, on a down count when the count reaches 0, it is reset to 255 on the next cycle. You can use GPIO numbering in this program by changing the following two statements:

```
~~~
int LEDs[] = {11, 9, 10, 22, 27, 17, 3, 2};

and

wiringPiSetupGpio()
~~~
```

### pigpio

The pigpio program of the project is shown in Figure 5.19 (Program: UpDown2.c). The program is the same as the wiringPi version with a few small modifications.

```
~~~c
/*----------------------------------------------------------------------
                    BINARY UP/DOWN COUNTER
                    =======================
In this program 8 LEDs are connected to GPIO ports through current
limiting resistors. Additionally, a button is used. The program counts
up/down in binary every 500ms. By default it counts up. When the
button is pressed it counts down as long as the button is kept pressed

In this version of the program the pigpio library is used

Author: Dogan Ibrahim
File : UpDown2.c
Date : December 2020
----------------------------------------------------------------------*/

#include <pigpio.h>
#include <stdio.h>

#define OFF 0
#define ON 1
#define Button 14
#define UP 0
#define DOWN 1

int LEDs[] = {11, 9, 10, 22, 27, 17, 3, 2};
~~~
//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
    char k;
    for(k = 0; k < 8; k++)
    {
        gpioSetMode(LEDs[k], PI_OUTPUT);
        gpioWrite(LEDs[k], OFF);
    }
    gpioSetMode(Button, PI_INPUT);
}

//
// Display data on ports
//
void Display(unsigned int No, unsigned int L)
{
    unsigned int j, i, m, p, r;
    m = L - 1;
    for(i = 0; i < L; i++)
    {
        j = 1;
        for(p = 0; p < m; p++)j = 2*j;
// Power of 2
        r = No & j;
        if(r > 0) r = 1;
        gpioWrite(LEDs[i], r);
        m--;
    }
}

//
// Start of MAIN program. When the button is not pressed,increment
// count. When the button is pressed, count down from the last value
//
int main(void)
{
    char j, count = 0;
    char Button_State;

    gpioInitialise();
    Configure();

while(1)
{
        Display(count, 8);
        Button_State = gpioRead(Button);

        if(Button_State == UP)
        {
                if(count == 255)
                        count = 0;
                else
                        count++;
        }
        else if(Button_State == DOWN)
        {
                if(count == 0)
                        count = 255;
                else
                        count--;
        }
        time_sleep(0.5);
}
```

Figure 5.19 Program UpDown2.c

## 5.6 • Project 5 – LED dice

### Description:

This is a simple dice project based on LEDs and a push-button switch. The LEDs are organised to simulate the look of the faces of real dice. When the push-button switch is pressed, a random number is generated between 1 and 6 and displayed on the LEDs. Normally the LEDs are all OFF to indicate that the system is ready to generate a new dice number. After 3 seconds the LEDs turn OFF again.

### Aim:

This project aims to show how an LED-based dice can be designed.

### Block diagram:

Figure 5.20 shows the block diagram of the project.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_136_0.png)

Figure 5.20 Block diagram of the project

As shown in Figure 5.21, the LEDs are organised such that when they turn ON, they indicate the numbers as in a real dice. The operation of the project is as follows: Normally the LEDs are all OFF to indicate that the system is ready to generate a new dice number. Pressing the switch generates a random dice number between 1 and 6 and displays on the LEDs for 3 seconds. After 3 seconds the LEDs turn OFF again.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_136_1.png)

Figure 5.21 LED dice

### Circuit diagram:

The circuit diagram of the project is shown in Figure 5.22. 7 LEDs are connected to GPIO pins 9, 10, 22, 27, 17, 3 and 2 through 470 Ohm current limiting resistors. The connection is as follows:

| LED | GPIO pin | wiringPi pin | Physical pin |
|---|---|---|---|
| D1 | 9 | 13 | 21 |
| D2 | 10 | 12 | 19 |
| D3 | 22 | 3 | 15 |
| D4 | 27 | 2 | 13 |
| D5 | 17 | 0 | 11 |
| D6 | 3 | 9 | 5 |
| D7 | 2 | 8 | 3 |

The push-button switch is connected to GPIO pin 14 through a 10K pull-down resistor so the button output is at logic 0 and goes to logic 1 when the button is pressed.
