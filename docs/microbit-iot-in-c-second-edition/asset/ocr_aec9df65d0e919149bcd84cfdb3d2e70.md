Using function t getting the five bytes is trivial:

```
uint32_t byte1 = getByte(1, buf);
uint32_t byte2 = getByte(2, buf);
uint32_t byte3 = getByte(3, buf);
uint32_t byte4 = getByte(4, buf);
uint32_t byte5 = getByte(5, buf);
```

The first two bytes are the humidity measurement, the second two the
tperature and the final byte is the checksum. The checksum is just the sum
of the first bytes reduced to 8 bits and we can test it using:
UBit.serial.printf("Checksum %%%%\n\r", byte5,
(byte1 + byte2 + byte3 + byte4) & 0xFF);

If the two values are different, then there is a transmission error.
In this case the simplest thing to do is get another reading from the device.
However, you shouldn't read the device more than once every 2 seconds.

The humidity and temperature are also easy to reconstruct as they are
transmitted high byte first and then the actual value. The only problem is
the microbit byte doesn't have floating point support and so it is
eier to keep the values as humidity*10 and temperature*10. The humidity
data is easy:

```
int16_t humidity = (byte << 8) | byte2;
```

The temperature data is slightly more difficult in that the topmost bit is used
to indicate a negative temperature. This isn't two's complement or any other
standard format. The most significant bit is used as a negative sign for
the value stored as a positive binary value in the lower-order bits.

This means we have to test for the most significant bit and flip the sign of the
tem if it is set:

```
int16_t temperature = (byte3 << 8) | byte4;
if(temperature & 0x8000)temperature=(temperature & 0x7FFF);
```

This completes the data processing. All that is left is showing the data to the
user. For testing it is good to send the data to the serial port so that it can be
checked:

```
UBit.serial.printf("Humidity %d%%\n\r",
humidity / 10, abs(humidity % 10));
UBit.serial.printf("Temperature %dC\n\r",
tem / 10, abs(temperature % 10));
```

Note the use of %% to display a percentage sign.