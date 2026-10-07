If you think about the hardware for a moment, it should be obvious that we can turn on any LED in a single row by setting its row on and multiple columns to off. However, notice that if we turn on an entire row or column, we are not free to turn on any other LED we like. For example, if you turn another column then the LED in the same row comes on, even if you don't want it to.

How then can we create a display where LEDs in different rows are on at the same time? The answer is that we turn off soft so that the human eye can see the flashing. For example, to turn the LEDs in column 3 and rows 1, 2 and 3 you could:

```
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

# micro:bit V2 LEDs

The micro:bit V2 doesn't have an mbed layer between it and the GPIO pins. The setDigitalValue method sets the GPIO line directly:

```
if(value) {
  PORT->OUTSET = 1 << PIN;
} else {
  PORT->OUTCLR = 1 << PIN;
}
```