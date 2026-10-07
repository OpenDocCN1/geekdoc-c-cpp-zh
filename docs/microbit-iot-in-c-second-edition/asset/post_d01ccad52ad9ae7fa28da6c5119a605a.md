
For example, to flash the middle LED we need a DigitalOut object from the mbed library.

| Function | Description |
| :--- | :--- |
| DigitalOut (PinName pin) | Create a DigitalOut connected to the specified pin |
| DigitalOut (PinName pin, value) | Create a DigitalOut connected to the specified pin with given initial value |

void write (int value) Set the output setting, specified as 0 or 1 (int)
int read ( ) Return the output setting, represented as 0 or 1 (int)
int is_connected () Return the output setting, represented as 0 or 1 (int)
DigitalOut & operator= (int value) A shorthand for write()
operator int () A shorthand for read()

All you need to make use of this is that there is also a complete set of pin names like P0_n for GPIO n. Using this you can access any GPIO line. In addition there are also predefined pin names for each of the columns and rows.

So to flash the center LED you would use:
```c++
#include "MicroBit.h"
MicroBit uBit;
int main() {
    uBit.init();
    uBit.display.disable();

DigitalOut col3(P0_6);
DigitalOut row2(P0_14);
while(1) {
    row2 = 1;
    wait(0.2);
    row2 = 0;
    wait(0.2);
}

release_fiber();
return 0;
}
```

Notice that to take control of the GPIO lines that work with the display you call its disable method. After this the program simply sets col3 to zero and toggles row2 to flash the LED. To specify the locations, we could equally well used:
DigitalOut col3(COL3,0);
DigitalOut row2(ROW2);
```

If you think about the hardware for a moment, it should be obvious that we can turn on any LED in a single row by setting its row on and multiple columns to off. However, notice that if we turn on an entire row or column, we are not free to turn on any other LED we like. For example, if you turn another column then the LED in the same row comes on, even if you don't want it to.

How then can we create a display where LEDs in different rows are on at the same time? The answer is that we turn off soft so that the human eye can see the flashing. For example, to turn the LEDs in column 3 and rows 1, 2 and 3 you could:

```c++
DigitalOut col3(COL3,0);
DigitalOut row1(ROW1);
DigitalOut row2(ROW2);
DigitalOut row3(ROW3);
while(1) {
  wait(0.2);
  row1 = 0;
  row2 = 1;
  wait(0.2);
  row2 = 0;
  row3 = 1;
  wait(0.2);
  row3 = 0;
}
```

If you run this program you will see the LEDs on the diagonal flash after another. Now take out the wait function calls - you will see the three LEDs on the diagonal all apparently at the same time. This is what the framework display object does for you automatically. It scans the three rows turning on and off LEDs in the framework's event handler. If you want to do this sort of job at a reasonable speed you need to set and unset all of the LEDs in a single row in one operation, as explained in Chapter 3. The mbed library has functions that you can use to do this or you can write yours.

## micro:bit V2 LEDs

The micro:bit V2 doesn't have an mbed layer between it and the GPIO pins. The setDigitalValue method sets the GPIO line directly:

```c++
if(value) {
  PORT->OUTSET = 1 << PIN;
} else {
  PORT->OUTCLR = 1 << PIN;
}
```

In this case we can set the GPIO lines connected to the LED display using the standard setDigitalValue method:

```c++
#include "MicroBit.h"
MicroBit uBit;
int main()
{
    uBit.init();
    uBit.display.disable();
    uBit.io.row3.setDigitalValue(1);

    while (1) {
        uBit.io.col3.setDigitalValue(1);
        uBit.sleep(100);
        uBit.io.col3.setDigitalValue(0);
        uBit.sleep(100);
    }

    release_fiber();
    return 0;
}
```

This allows us to turn a single LED at a given row and column. As in the case of micro:bit, once we switch a single LED on are not free to turn any other LED. If a particular row and column is activated then setting another column turns the LED in the original row on, even if the LED we want to turn on. The solution is to ever turn a single LED at a time and to do this quickly for the user to see multiple on.

```c++
#include "MicroBit.h"
MicroBit uBit;
int main()
{
    uBit.init();
    uBit.display.disable();

    while (1) {
        uBit.io.col1.setDigitalValue(0);
        uBit.io.row1.setDigitalValue(1);
        uBit.sleep(500);
        uBit.io.col1.setDigitalValue(1);
        uBit.io.row1.setDigitalValue(0);
        uBit.io.col2.setDigitalValue(0);
        uBit.io.row2.setDigitalValue(1);
        uBit.sleep(500);
    }
}
```

```c++
uBit.io.col2.setDigitalValue(1);
uBit.io.row2.setDigitalValue(0);
uBit.io.col3.setDigitalValue(0);
uBit.io.row3.setDigitalValue(1);
uBit.sleep(500);
uBit.io.col3.setDigitalValue(1);
uBit.io.row3.setDigitalValue(0);
uBit.io.col4.setDigitalValue(0);
uBit.io.row4.setDigitalValue(1);
uBit.sleep(500);
uBit.io.col4.setDigitalValue(1);
uBit.io.row4.setDigitalValue(0);
uBit.io.col5.setDigitalValue(0);
uBit.io.row5.setDigitalValue(1);
uBit.sleep(500);
uBit.io.col5.setDigitalValue(1);
uBit.io.row5.setDigitalValue(0);
}

release_fiber();
return 0;
```

If you run this program with sleep(500) then you will see a dot moving along the diagonal. If you remove the sleep function calls you will see a solid diagonal.

## Greyscale

One of the features of the framework's support for the LED display that isn't so obvious is that you can use it as a greyscale display. The reason it isn't obvious is that there isn't a setValue for a single LED. The framework doesn't have any functions that work with a single LED at all. However, the display object uses a buffer which is a MicroBitImage object. The basic idea is that you can create MicroBitImage objects and print them to the display or you work directly with the buffer MicroBitImage object to display "live" graphics.

The key method is:
`setPixelValue(int16_t x,int16_t y,uint8_t value)`
where value can be anything from 0 to 255.

The brightness is created by simply turning the LED on and off in the correct ratio as in PWM, although PWM isn't used in the display. It is a simple consequence of the repeated rendering of the display and the percentage of time a pixel is set to on.

For example, you can slowly increase the brightness of the center LED:
```c++
uBit.init();
uBit.display.setDisplayMode(DISPLAY_MODE_GRESCALE);
int i;
for(i=0;i<256;i++){
  uBit.display.image.setPixelValue(2,2,i);
  uBit.sleep(50);
}
```

Notice that you have to set the greyscale mode because this is more complex and not the default. You can explore the possibilities of using MicroBitImage object to perform animation and other graphical techniques. The real problem, however, is that no matter how clever your software you only have a 5x5 display.

## Using Aliasing to Increase Resolution

As an example of how you can use the grey-level resolution of the display to increase its effective spatial resolution, let's implement a traditional BBC Micro game - Command Jump. This is a very simple game where a figure's height above the baseline is controlled by how fast the user clicks a button. Only showing five positions makes it a little crude.

As an alternative to moving the command by one LED for every 10 button clicks, we can move the brightness from one to another gradually. You can think of this as locating the commando in the gaps between the LED, but it is also the standard anti-aliasing technique from higher resolution graphics.

A function to move the command by fractional amounts is:

```c++
void flashMan(int x, int y, int p, int vx, int vy) {
  uBit.display.image.setPixelValue(x, y, 0);
  uBit.display.image.setPixelValue(x + vx, y + vy, 0);
  uBit.sleep(100);
  uBit.display.image.setPixelValue(x, y, 25 * (10 - p));
  uBit.display.image.setPixelValue(x + vx, y + vy, 25 * p);
  uBit.sleep(100);
}
```

The command is at x, y and p is used to indicate how close it is to being at x+vx and y+vy. For example, suppose p is 0 then the first LED is set to 10*25, ni.e. 250, and the second to 0. If p is 3 then the first is set to 7*25 and the second to 3*25. Finally, if p is 10 the first is set to 0 and the second to 10*25.
