```
```c
gcc -o FadeLED FadeLED.c -lwiringPi -lpthread

/*-------------------------------------------------------------
                         CHANGING LED BRIGHTNESS
                         =======================
In this program an LED is connected to GPIO 2. The brightness of
the LED is changed using PWM waveform

Author : Dogan Ibrahim
File   : FadeLED.c
Date   : December 2020
-------------------------------------------------------------*/
#include <wiringPi.h>
#include <softPwm.h>

#define LED 8                              // GPIO 2

//
// Configure LED port as output
//
void Configure()
{
        pinMode(LED, OUTPUT);              // LED output
        digitalWrite(LED, LOW);            // LED OFF
}

//
// Start of MAIN program
//
int main(void)
{
        int k;

        wiringPiSetup();
        Configure();
        softPwmCreate(LED, 0, 200);        // PWM T=20ms

        while(1)
        {
                for(k = 0; k <= 200; k++)              // Increase brightness
                {
                        softPwmWrite(LED, k);
                        delay(25);                      // 25ms delay
                }

                for(k = 200; k >= 0; k--)              // Decrease brightness
```
```