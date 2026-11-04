```
/*-----------------------------------------------------------
GENERATE TONE WITH KEYBOARD FERQUENCY
========================================

In this program a passive buzzer is connected to GPIO 2. The program
reads the required frequency from the keyboard

Author: Dogan Ibrahim
File : tone2.c
Date : December 2020
-----------------------------------------------------------*/

#include <wiringPi.h>
#include <softTone.h>
#include <stdio.h>
#include <stdlib.h>

#define Buzzer 2                 // Buzzer at GPIO 2

//
// Start of MAIN program
//
int main(void)
{
    int freq;
    char buff[50];

    wiringPiSetupGpio();
    softToneCreate(Buzzer);

    while(1)
    {
        printf("\n\nEnter frequency (0 to exit - Max 5000Hz): ");
        freq = atoi(fgets(buff,10,stdin));
        if(freq == 0)break;
        printf("Generating tone at freq = %d Hz", freq);
        softToneWrite(Buzzer, freq);
    }

    softToneWrite(Buzzer, 0);
    delay(1000);
    printf("End of program\n");
}
```

Figure 12.11 Program tone2.c

An example run of the program is shown in Figure 12.12.