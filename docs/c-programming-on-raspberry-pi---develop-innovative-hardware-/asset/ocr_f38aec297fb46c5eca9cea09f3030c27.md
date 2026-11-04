![](bbox=[0.26, 0.09, 0.78, 0.38])

Figure 8.6 Circuit diagram of the project

# Program listing:

# wiringPi

wiringPi includes the MCP23S17 chip library which makes programming the chip very easy. The header file `<mcp23s17.h>` must be included at the beginning of the program. The SPI bus must be initialised using the following function:

```
mcp23s17Setup(Base, CE, address)
```

Base is an index that is used to identify the port pins and it must be greater than 64. CE is the chip enable pin used (0 for CE0 i.e. we are using GPIO 8, and 1 for CE1, i.e. we are using GPIO 7), address is the address of the chip (0 in this project). The pinMode and digitalWrite functions can then be used to configure and access the port pins. For example, if Base = 100, then `digitalWrite(100, 1)` will set GPA0 to logic 1, `digitalWrite(101, 1)` will set GPA1 to logic 1 and so on.

Figure 8.7 shows the program listing (Program: SPILED.c). Notice that in this project, the SPI bus is initialised as:

```
mcp23s17Setup(Base, CE, 0);
```

Where Base = 100, and CE = 0.

Pin GPA0 (index = 100) is configured as an output and a while loop is formed. Inside this loop, this port is set to logic 1, and then to logic 0 with a one-second delay between each output.