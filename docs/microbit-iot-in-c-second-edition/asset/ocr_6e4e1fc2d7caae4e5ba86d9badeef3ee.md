Overall it is easier to work with a scaled integer - in this case temperature times 100 - so multiply the expression for temperature by 100 and make use of the fact that dividing by 2^16 is the same as 16 right shifts:
int temp= -4685((17572*data16))>>16);

Now all we have to do is print the temperature as a correctly scaled value:

```
printf("Temperature %d.%d C \n\r",temp/100,temp%100);
```

The final program:
#include "MicroBit.h"
MicroBit uBit;

```
int main() {
	uBit.init();
	uint8_t buf[3] = {0};
	uBit.i2c.readRegister(0x80, 0xE3, buf, 3);
	uint8_t msb = buf[0];
	uint8_t lsb = buf[1];
	uint8_t check = buf[2];

unsigned int data16 = ((unsigned int)msb << 8) | ((unsigned int)lsb & 0FC);
int temp = -4685 + ((17572 * data16) >> 16);
tuBit.serial.printf("Temperature %d.%d C \n\r", temp / 100, temp % 100);

return 0;
}
```

# Reading the Humidity

The nice about I2C and using a particular I2C device is that it gets easier. Once you have seen how to do it with one device, the skill generalizes and you know how to deal with a particular device other aspects of the device are usually similar.

To read the humidity we can or less use the same program, we just need to change the command and the formula for the final percentage humidity. The command needed to read the three data bytes is 0xE5 and the formula to convert the 16-bit value to percentage relative humidity (RH) is:

```
-6 + 125 * data16 / 2^16
```

This can be implemented in integer arithmetic if we work with RH*100.