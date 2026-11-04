```
/*--------------------------------------------------------------------------------
I2C LCD
======
In this program an PCF8574 based I2C LCD is connected to Raspberry Pi.
The program displays text Raspberry Pi on the LCD.

Author: Dogan Ibrahim
File  : I2CLCD.c
Date  : December 2020
--------------------------------------------------------------------------------*/

#include <wiringPi.h>
#include <pcf8574.h>

#define DeviceAddress 0x27          // Device addr
#define PCF 100                     // Port offset

#define RS PCF+0                    // RS pin
#define RW PCF+1                    // RW pin
#define E PCF+2                     // E pin
#define LED PCF+3                   // Backlight
#define D4 PCF+4                    // D4 pin
#define D5 PCF+5                    // D5 pin
#define D6 PCF+6                    // D6 pin
#define D7 PCF+7                    // D7 pin

int handle;
void lcd_strobe(void);

void lcd_write(unsigned char c, int mode)    //0=cmd,1=data
{
    unsigned char d, b,i;
    d = c;
    d = (d >> 4);                   // Upper nibble
    for(i = 0; i < 4; i++)
    {
        b = d & 1;
        digitalWrite(PCF+4+i,b);    // Set pins
        d = d >> 1;
    }
    digitalWrite(RS, mode);
    lcd_strobe();

    d = c;
    for(i = 0; i < 4; i++)
    {

```