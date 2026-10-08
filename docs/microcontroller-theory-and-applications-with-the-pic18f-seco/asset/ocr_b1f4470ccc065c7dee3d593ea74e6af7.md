```
```

I2C_Master_Wait();
SSPCON2bits.SEN = 1;
}
void I2C_Master_Stop()
{
I2C_Master_Wait();
SSPCON2bits.PEN = 1;
}
void I2C_Master_Write(unsigned char writeData)
{
I2C_Master_Wait();
SSPBUF = writeData;
}
void main()
{
ADCON1 = 0x0F;
// PORTB as input
I2C_Master_Init(100000);
// 100kHz baud rate
while(1)
{
I2C_Master_Start();
//Start condition
I2C_Master_Write(SLAVE_ADDRESS);
// 7 bit address + Write
I2C_Master_Write(PORTB);
// Write data
I2C_Master_Stop();
// Stop condition
}
```

```