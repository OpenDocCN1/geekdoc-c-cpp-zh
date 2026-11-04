
## 7.3 ● Project 1 – Port expander

### Description:
A simple project is given in this section to show how I2C functions can be used in a program. In this project, the I2C bus compatible Port Expander chip (MCP23017) is used to give an additional 16 I/O ports to the Raspberry Pi. This is useful in some applications where a large number of I/O ports are required. In this project, an LED is connected to MCP23017 port GPA0 (pin 21) and the LED is flashed ON and OFF every second so the operation of the program can be validated. A 470 Ohm current limiting resistor is used in series with the LED.

### Aim:
This project aims to show how the I2C bus can be used in Raspberry Pi projects.

### Block diagram:
The block diagram of the project is shown in Figure 7.2.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_201_0.png)

### The MCP23017
The MCP23017 is a 28-pin chip with the following features. Pin configuration is shown in Figure 7.3:

- 16 bi-directional I/O ports.
- Up to 1.7MHz operation on the I2C bus.
- Interrupt capability.
- External reset input.
- Low standby current.
- +1.8 to +5.5V operation.
- 3 address pins so that up to 8 devices can be used on the I2C bus.
- 28-pin DIL package.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_202_0.png)

Figure 7.3 Pin configuration of the MCP23017

Pin descriptions are given in Table 7.1.

| Pin | Description |
|---|---|
| GPA0–GPA7 | Port A pins |
| GPB0–GPB7 | Port B pins |
| VDD | Power supply |
| VSS | Ground |
| SDA | I2C data pin |
| SCL | I2C clock pin |
| RESET | Reset pin |
| A0–A2 | I2C address pins |

Table 7.1 MCP23017 pin descriptions

The MCP23017 is addressed using pins A0 to A2. Table 7.2 shows the address selection. In this project, address pins are connected to ground, thus the address of the chip is 0x20. The chip address is 7 bits wide with the low bit set or cleared depending on whether we wish to read data from the chip or write data to the chip respectively. Since in this project we will be writing to the MCP23017, the low bit should be 0, making the chip byte address (also called the **device opcode**) 0x40.

| A2 | A1 | A0 | Address |
|---|---|---|---|
| 0 | 0 | 0 | 0x40 |
| 0 | 0 | 1 | 0x21 |
| 0 | 1 | 0 | 0x22 |
| 0 | 1 | 1 | 0x23 |
| 1 | 0 | 0 | 0x24 |
| 1 | 0 | 1 | 0x25 |
| 1 | 1 | 0 | 0x26 |
| 1 | 1 | 1 | 0x27 |

Table 7.2 Selecting address of the MCP23017

The MCP23017 chip has 8 internal registers that can be configured for its operation. The device can be operated either in 16-bit mode or two 8-bit mode by configuring bit IOCON. BANK. On power-up, this bit is cleared which selects the two 8-bit mode by default.

The I/O direction of the port pins are controlled with registers IODIRA (at address 0x00) and IODIRB (at address 0x01). Clearing a bit to 0 in these registers makes the corresponding port pin(s) as output(s). Similarly, setting a bit to 1 in these registers makes the corresponding port pin(s) inputs. GPIOA and GPIOB register addresses are 0x12 and 0x13 respectively. This is shown in Figure 7.4.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_203_0.png)

Figure 7.4 Configuring the I/O ports

Figure 7.5 shows the circuit diagram of the project. Notice the I2C pins of the port expander are connected to pins GPIO 2 (SDA) and GPIO 3 (SCL) of the Raspberry Pi and are pulled-up using 10K resistors as required by the I2C specifications. The LED is connected to port pin GPA0 of the MCP23017 (pin 21). The address select bits of the MCP23017 are all connected to ground.

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_204_0.png)

Figure 7.5 Circuit diagram of the project

More information on the MCP23017 chip can be obtained from the datasheet:

https://ww1.microchip.com/downloads/en/devicedoc/20001952c.pdf

## Program listing:

### wiringPi
The header file **<wiringPiI2C.h>** must be included at the beginning of the program and the program must be linked with the library: **-lwiringPi**.

wiringPi supports the following I2C functions (for full details, see link: http://wiringpi.com/reference/i2c-library/ ):

**wiringPiI2CSetup(devID):** this function initialises the I2C bus with the specified device address (use **i2cdetect** to find out this address). An integer filehandle is returned (or -1 if an error is detected)

**wiringPiI2CRead(handle):** this function reads data from the device

**wiringPiI2CWrite(handle, data):** this function writes data to the device to write 8 or 16-bit data, use:

**wiringPiI2CWriteReg8(handle, reg, data)**  
**wiringPiI2CWriteReg16(handle, reg, data)**

to read 8 or 16-bit data, use:

**wiringPiI2CReadReg8(handle, reg);**  
**wiringPiI2CReadReg16(handle, reg);**

After building the circuit, the device address was checked and was found to be 0x20 as shown in Figure 7.6.

```
pi@raspberrypi:~ $ sudo i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: 20 -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
```

Figure 7.6 MCP23017 device address

GPIO pin numbering is used in this program. Figure 7.7 shows the program listing (Program: **I2Cexpander.c**). The wiringPi library supports the MCP23017 chip directly and therefore there is no need to use the I2C functions to communicate with the chip. The header file **<mcp23017.h>** must be included at the beginning of the program. The chip is then initialised by calling function **mcp23017Setup**. This function has two arguments: **pinBase** and **DEVICE_ADDRESS**. The **pinBase** must be above 64. This number is used to address the I/O ports of the chip. The chip has 16 I/O ports (GPIOA and GPIOB). pinBase+1 corresponds to port pin GPA0, pinBase+2 corresponds to port pin GPA1, and so on. For example, if the pinBase is set to 100, the I/O pins are addressed as follows:

- 100 GPA0
- 101 GPA1
- 102 GPA2
- ..............
- 107 GPA7
- 108 GPB0
- 109 GPB1
- ..............
- 114 GPB7

In this project, the **DEVICE_ADDRESS** of the chip is 0x20. The program configures all 8 ports GPA0 – GPA7 to outputs and then turns ON and OFF port pin GPA0 every second. You can compile and run the program as follows:

```
gcc -o I2Cexpander I2Cexpander.c -lwiringPi
sudo ./I2Cexpander
```

```c
/*--------------------------------------------------------------
                         MCP23017 I2C LED FLASH
                         ======================

In this program an LED is connected to MCP23017 chip which is an I2C
based chip. The program flashes the LED every second

Author: Dogan Ibrahim
File   : I2CExpander.c
Date   : December 2020
--------------------------------------------------------------*/
#include <wiringPi.h>
#include <lcd.h>
#include <mcp23017.h>

#define DEVICE_ADDRESS 0x20

//
// Start of MAIN program
//
int main(void)
{
                int i;

                wiringPiSetup();
                mcp23017Setup(100, DEVICE_ADDRESS);

                for(i = 0; i < 8; i++)pinMode(100+i, OUTPUT);
                while(1)
                {
                                digitalWrite(100, 1);
                                delay(1000);
                                digitalWrite(100, 0);
                                delay(1000);
                }
}
```

Figure 7.7 Program I2CExpander.c

## Using I2C functions
The program given in Figure 7.7 uses the built-in MCP23017 library. The program listing shown in Figure 7.8 (Program: **I2CExpander2.c**) uses the I2C functions. At the beginning of the program, header file **<wiringPiI2C.h>** is included in the program. The MCP23017 device address is defined as 0x20. The **GPIOA** register address and **IODIRA** port direction register address are defined as 0x12 and 0x00 respectively (see Figure 7.4). The I2C bus is initialized by calling function wiringPiI2CSetup which returns integer **handle**. All 8 **GPA0**
