# **Program Listing:**

# **wiringPi**

Figure 10.8 shows the program listing (program: **sawtooth.c**). The program is very similar to the one given in Figure 10.4. Function **DAC** sends data to the DAC converter. Inside the main program loop, variable *i* is incremented from 0 to 1.0 in steps of 0.1, and a 0.1ms delay is inserted between each output.

```
```c
/*----------------------------------------------------------
                    GENERATING SAWTOOTH WAVE SIGNAL USING DAC
                    =========================================

In this project an analogue-to-digital converter is used to generate
sawtooth wave signal. The peak value of the signal is set to 3.3V. The
step width is 1ms and there are 6 steps per period

Author: Dogan Ibrahim
File   : sawtooth.c
Date   : December 2020
------------------------------------------------------------*/
#include <wiringPiSPI.h>
#include <wiringPi.h>
#include <stdio.h>
#define channel 0                                      // Use CE0

int handle;

//
// Send data to the DAC chip, HIGH byte first
//
void DAC(int data)
{
        char buff[2];

        buff[0] = (data >> 8) & 0x0F;
        buff[0] = buff[0] + 0x30;                     // HIGH byte
        buff[1] = data & 0xFF;                         // LOW byte
        wiringPiSPIDataRW(handle, buff, 2);            // Send
}

//
// Start of MAIN program
//
int main(void)
{
```
```