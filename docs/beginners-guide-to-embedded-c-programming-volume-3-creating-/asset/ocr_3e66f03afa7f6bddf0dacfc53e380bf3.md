```
// i2c_write - write unsigned char - returns ACK
//
//**********************************************************
void i2c_init()
{
TRISC3=1;      // set SCL and SDA pins as inputs
TRISC4=1;
SSPCON = 0x38;  // set I2C master mode
SSPCON2 = 0x00;
// Formula for SSPADD register value: SSPADD = [(Fosc/4)/BitRate] - 1
SSPADD = 0x27;   // 100K at 16Mhz clock
                 // [(16Mhz/4)/100khz]-1 = 39 or 0x27 hex

SMP=1;           // disable slew rate control for 100khz operation
SSPIF=0;         // clear SSPIF interrupt flag
BCLIF=0;         // clear bus collision flag
}
```

You have to make sure the I2C bus is ready for transmit or receive so a function to test the status bits is handled with the i2c_waitForIdle routine.

```
//**********************************************************
void i2c_waitForIdle()
{
while ((SSPCON2 & 0x1F ) | RW ){}; // wait for idle and not writing
}
```

An I2C start bit is created with the i2c_start( ) function.

```
//**********************************************************
void i2c_start()
{
i2c_waitForIdle();
SEN=1;
}
```

An I2C repeat start bit is created with the i2c_repstart( ) function.

```
//**********************************************************
void i2c_repStart()
{
i2c_waitForIdle();
RSEN=1;
}
```