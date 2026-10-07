Putting all together and reusing some variables from the previous program, we have:
uubit.i2c.readRegister(0x80, 0xE5, buf, 3);
msb = buf[0];
lsb = buf[1];
check = buf[2];
uBit.serial.printf("n\rmsb %d \n\rlsb %d \nrchecksum %d \n\r", msb, lsb, check);
data16 = ((unsigned int)msb << 8) | (unsigned int) (lsb & 0xFC);
hint hum = -600 + (12500 * data16) >> 16;
uBit.serial.printf("Humidity %d %% %d \\n", hum / 100, hum % 100);

The only unusual part of the program is using %%% to print a single character - necessary because %%% already means something in printf.

# Checksum Calculation

Although computing a checksum or cyclic redundancy check (CRC), which is used to detect accidental changes to raw data not specific to I2C, it is another common task. The datasheet explains that the polynomial used for the CRC is:

X^8+X^3+X^4+X+1

Once you have this information you can work out the divisor by writing a binary number with a one in each location corresponding to a power of X in the polynomial, i.e the 8th, 5th, 4th and 1st bit. Hence the divisor is 0x031.

What you do next is roughly the same for all CRCs. First you put the data that was used to compute the checksum together with the checksum value as the lower-order bits:

```
uint32_t data32 = ((uint32_t)msb << 16) | |
(uint32_t) lsb << 8) | (uint32_t) check;
```

Now you have three bytes, ie 24 bits, in a 32-bit variable.

Next adjust the divisor so that its most significant non-zero bit aligns with the most significant bit of the three bytes. As this divisor has one at bit it needs to be shifted 15 places to move it to the 24th bit:

```
uint32_t divisor = ((uint32_t) 0x0131) <<15;
```

Now that you have both the data and the divisor aligned, you step through the top-most 16 bits, i.e. you don't process the low-order eight bits which is the received checksum.