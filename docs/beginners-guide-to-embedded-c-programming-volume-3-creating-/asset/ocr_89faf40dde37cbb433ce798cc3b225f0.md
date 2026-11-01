```
SSPPBUF = I2CwriteData;
return ( ! ACKSTAT ); // function returns '1' if transmission is acknowledged
}
// ******************************************
// I2C EEOUT function to write to an 8-bit address Microchip
// EEPROM part (i.e. 24LC01) with 8 byte address (2k bit max)
// ******************************************
```

Probably the most common use of I2C is communicating with EEPROM so I wrote the I2C_EEOUT () and I2C_EEIN () functions to handle this communication using the functions I previously described. You can use these as the format for future I2C communication as they are all very familiar.

```
void I2C_EEOUT(unsigned char address, unsigned char data)
{
    i2c_start();
    i2c_write(0xa0);
    i2c_write(address);
    i2c_write(data);
    i2c_stop();
    pause(11);
}
```

```
// ******************************************
// I2C EEIN function to read from an 8-bit address Microchip
// EEPROM part (i.e. 24LC01) with 8 byte address (2k bit max)
// ******************************************
```

```
unsigned char I2C_EEIN(unsigned char address)
{
    unsigned char data;

    i2c_start();
    i2c_write(0xa0);
    i2c_write(address);
    i2c_repStart();
    i2c_write(0xa1);
    data=i2c_read(0);
    i2c_stop();
    return(data);
}
```

You should now have a basic understanding and reference of what options you have when using the SimpleC library. Now let me use the rest of the book to show you how easy this library makes programming the PIC16F886 in the CHIPINO module. Some of these projects are repeats of the projects in Volume 1 and Volume 2 of this book series but you will see they are much quicker to write and much easier to understand.