```
```c
#include <pigpio.h>
#include <stdlib.h>

#define R 17                  // GPIO 17
#define G 27                  // GPIO 27
#define B 22                  // GPIO 22

//
// Configure LED ports as outputs
//
void Configure()
{
    gpioSetMode(R, PI_OUTPUT);    // Red port
    gpioSetMode(G, PI_OUTPUT);    // Green port
    gpioSetMode(B, PI_OUTPUT);    // Blue por
}

//
// Start of MAIN program
//
int main(void)
{
    int Red, Green, Blue;

    gpioInitialise();
    Configure();

    while(1)
    {
        Red = rand() % 2;         // Between 0,1
        Green = rand() %2;        // Between 0,1
        Blue = rand() %2;         // Between 0,1

        gpioWrite(R, Red);        // Red ON/OFF
        gpioWrite(G, Green);      // Green ON/OFF
        gpioWrite(B, Blue);       // Blue ON/OFF
        time_sleep(0.2);          // 200 ms delay
    }
}
```
```

Figure 5.31 Program RGB2.c

# Suggestions:

In the program described in Figure 5.30 and 5.31, the delay time is set to 200 ms. Try changing this time and see its effects.