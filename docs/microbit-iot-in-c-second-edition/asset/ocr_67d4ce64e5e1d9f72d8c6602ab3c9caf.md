If you run the program you will see:
Register = 02

This is the default value of the register and it corresponds to a resolution of 12 and 14 bits for the humidity and temperature respectively and a supply voltage greater than 2.25V.

The same program can be written more compactly and more correctly using readRegister:

```
#include "MicroBit.h"
MicroBit uBit;
int main() {
  uBit.init();
  uint8_t buf[] = {0};
  uBit.i2c.readRegister(0x80, 0xE7, buf, 1);
  uBit.serial.printf("User Register = %X \r\n", buf[0]);
  return 0;
}
```

# The I2C Protocol In Action

If you have a logic analyzer that can interpret the I2C protocol connected, what you will see is:

![](bbox=[0.131, 0.502, 0.814, 0.706])

You can see that the write byte function sends an address packet set to the device's 7-bit address 0x40 as the high-order bits and the low-order bit set to zero to indicate a write. After this you get a data packet containing the address of the register, 0xE7. After a few microseconds, it sends the address frame again, only this time with the low-order bit set to 1 to indicate a read and it then receives back a single byte of data from the device, 0x02.