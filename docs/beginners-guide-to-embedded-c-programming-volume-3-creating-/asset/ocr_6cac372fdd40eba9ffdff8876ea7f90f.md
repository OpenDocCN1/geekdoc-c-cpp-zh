```
{
    i2c_start();
    i2c_write(0xa0);
    i2c_write(address);
    i2c_write(data);
    i2c_stop();
    pause(1);
}

// *******************************************************
// I2C_EEIN function to read from an 8-bit address Microchip
// EEPROM part (i.e. 24LC01) with 8 byte address (2K bit max)
// *******************************************************

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

// *******************************************************
//  Main Program Loop
// *******************************************************

void
main(void)
{
    init_micro();// Initialize I/O
    i2c_init();        // Initialize I2C
    PORTB=0x00;        // All LEDs off
    TRISB=0x00;        // All PORTB outputs

    unsigned char cnt=0;        // Create variable and initialize to zero

    while(cnt<=10)  /* write 10 numbers to eeprom */
    {
        PORTB=cnt;              // The cnt value will display on the LEDs
        I2C_EEOUT(cnt,10-cnt);  // Store 9 at address 1, 8 at address 2, ...
        cnt=cnt+1;              // Increment cnt variable
        pause(255);             // Delay 255 milliseconds
    }

    cnt=0;

    while(cnt<=10)
    {
        PORTB = I2C_EEIN(cnt); // Display data read from EEPROM on LEDs in binary
        pause (1000);         // Delay for 1 second to read LEDs
        cnt=cnt + 1;           // Increment cnt variable
    }
}
```