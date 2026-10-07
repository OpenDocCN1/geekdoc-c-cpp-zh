Now the data is ready to read and we can read all nine bytes of it or just the first two. The device will keep track of where the read is, so if you come back later and read bytes the first one will not be read again. If you issue an initialization pulse then the device aborts the data transmission.

We only need the first two bytes, which are the least and most significant bytes of 11-bit temperature reading as a 16-bit, two's complement integer.

```
int b1 = readByte();
int b2 = readByte();
```

# Getting the Temperature

All we now have to do is to put the two bytes together as a 16-bit integer. As the microbit:supports a 16-bit int, we can do this very easily:

```
int16_t temp = (b2<<8 | b1);
```

Finally we need to convert this to a floating point value. As already discussed, the microbit:doesn't support this in hardware. As we all really want to give digits to the tens and two digits to get the fractional part, it is easier to work in integer arithmetic using temperature multiplied by 100:

```
temp = temp * 100 / 16;
```

This gives an integer value that represents the temperature in hundreds of a degree centigrade, e.g. 25.45°C is represented as 2545. Notice that this only works because int16_t really is a 16-bit integer. If you were to use a 32-bit int:

```
int temp = (b2<<8 | b1);
```

then temp would be correct for positive temperatures, but it would give the wrong answer for negative values because the sign isn't propagated into the 10 bits. If using a 32-bit integer, propagate the sign bit manually:

```
if(b2 & 0x80) temp = temp | 0xFFFF0000;
```

Assuming we have the temperature in 100ths of a degree C in temp, we can show it on the microbit:s LED matrix. First we need to convert it into a string:

```
char buff[10];
sprintf(buff, "%d.%d", temp / 100, abs(temp % 100));
```

Now we can display the string:

```
uBit.display.scroll(buff, 200);
```

That finalizes a basic program to read the temperature and create some useful 1-wire functions. The next task would be to create a function that reads the temperature to refactor of code to demand.